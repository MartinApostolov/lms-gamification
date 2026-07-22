# Course Progress

> **Document status:** Rough functional outline grounded in the supplied LMS mock-up. Names, thresholds, rewards, interface details, and technical structures remain provisional.

## 1. What

Course Progress shows how much meaningful work a learner has completed in a particular Course Instance and identifies the next useful action.

Progress belongs to:

```text
User + CourseInstance
```

The learner view should show:

- required progress from 0% to 100%;
- optional progress from 0% to 100% when optional activities exist;
- combined progress from 0 to 200 points when both values are shown;
- completed and remaining activities;
- the next recommended action;
- the separate existing academic Course-completion state.

The combined value is not “200% Course completion.” Optional work never blocks normal completion.

## 2. Current LMS grounding

### Confirmed current source

A Course Instance may have `isTracked: true`. Its copied curriculum lessons contain `completedBy` entries with learner and timestamp. The Course Details frontend uses this data to show completed lessons and the next incomplete lesson.

### Separate academic completion rule

The current LMS records successful Course completion only after the learner has a passing result for every exam attached to the Course Instance. Lesson progress must not overwrite, simulate, or contradict that record.

### Missing classification

The current schema does not identify a lesson as required or optional. The gamification extension must add configuration rather than infer importance from order, content type, or whether an assessment is attached.

## 3. Why

Visible progress and a clear next step can reduce abandonment between enrollment and the final exam without encouraging extra website use. The feature should help learners:

- begin the Course;
- understand their current stage;
- recover after falling behind;
- prepare for exams;
- complete required learning work;
- optionally explore additional material.

## 4. Calculation

### 4.1 Required progress

For the initial implementation:

```text
Unique required activities completed
------------------------------------ × 100
Total active required activities
```

Tracked lessons are the first supported activity type after the completion source is hardened. Assessment or challenge activities may be added only when their own source is trusted and explicitly configured as required.

### 4.2 Optional progress

```text
Unique optional activities completed
------------------------------------ × 100
Total active optional activities
```

Optional activities may include extra practice, exploration, or approved Collaborative Challenges. When none exist, optional and combined values may be hidden.

### 4.3 Combined progress

```text
Required percentage points + Optional percentage points
```

Example:

```text
Required: 75 / 100
Optional: 40 / 100
Total:    115 / 200
```

### 4.4 De-duplication

A completion counts once per configured requirement and learner. Existing lesson completion arrays must be normalized by:

```text
CourseInstance + lesson + learner
```

Multiple embedded completion rows for that identity still count as one completed lesson.

## 5. Next recommended action

Normal priority:

1. available incomplete required activity;
2. time-sensitive required activity;
3. incomplete Final Exam Readiness condition;
4. optional activity;
5. completed-state guidance such as exam details or refresher availability.

The action should deep-link to the existing Course Details lesson, assessment, exam, Study Group, or Challenge where possible.

## 6. Recalculation and events

Recalculate when:

- a trusted completion is added, corrected, or revoked;
- an activity changes required/optional status;
- a requirement becomes active/inactive;
- Course curriculum or Course Instance scope changes;
- a learner's enrollment changes.

Proposed events:

- `REQUIRED_PROGRESS_UPDATED`;
- `OPTIONAL_PROGRESS_UPDATED`;
- `COURSE_PROGRESS_RECALCULATED`.

The underlying LMS completion/result remains authoritative. A progress summary may cache a calculated display value.

## 7. Integration safety requirement

Before lesson completion can produce reward-capable events, the backend must:

- derive self-service learner identity from the authenticated token;
- verify Course Instance enrollment;
- enforce the completion rule server-side;
- prevent more than one completion identity per learner and lesson;
- return idempotently on replay;
- record authorized corrections and their actor/reason.

Until then, existing `completedBy` data may be used for a de-duplicated mock-up progress display but not as direct XP evidence.

## 8. Live-course behavior

- Scheduled dates do not prove attendance or lesson completion.
- No penalty is applied for not visiting the LMS between live sessions.
- Cancelled/rescheduled activities use corrected requirements and dates.
- Late enrollment shows remaining and recoverable requirements without granting earlier credit.
- Attendance contributes only when a reliable future attendance source exists.

## 9. Self-paced behavior

- Progress depends on completed requirements, not calendar activity.
- Several activities may be completed in one session.
- Inactivity does not reduce earned progress.
- Reopening content does not add progress.
- Deadlines apply only when explicitly configured.

## 10. Rules and edge cases

- Required and optional values remain between 0 and 100.
- Combined points remain between 0 and 200.
- Optional activity cannot satisfy a required condition unless it is independently configured as an alternative.
- A Course Instance has separate progress from another instance.
- The existing Course-template completion record may already be present from another instance; the UI must distinguish “Course already completed” from progress in the current instance.
- Corrections may reduce progress and must be auditable.
- Material requirement changes must define whether they affect already completed learners.
- Detailed progress is private to the learner and authorized staff.

## 11. Acceptance criteria

### AC1 — Initial progress

Given an enrolled learner has no trusted completion,
when progress is calculated,
then required progress is 0%
and the first available required action is shown.

### AC2 — Unique lesson calculation

Given 12 required lessons
and completion data contains 9 distinct completed lessons for the learner,
when progress is calculated,
then required progress is 75%, even if one lesson contains duplicate completion rows.

### AC3 — Optional separation

Given required progress is 80%
and optional progress is 100%,
when progress is evaluated,
then optional completion does not mark the required work complete.

### AC4 — Academic completion separation

Given required lesson progress reaches 100%
but one attached exam is not passed,
when the learner view is displayed,
then learning progress may show 100%
but the existing successful-Course state is not fabricated.

### AC5 — Idempotent source event

Given a lesson completion occurrence was already processed,
when the same occurrence is replayed,
then progress, XP, and milestones do not increase.

### AC6 — Separate Course Instance

Given the learner completed another instance of the same Course,
when viewing the new instance,
then its instance progress is separate
and the prior Course-level completion is displayed as contextual information only.

## 12. Data and model extensions

### Existing data

- User and Course Instance enrollment;
- `isLive` and `isTracked`;
- lesson `completedBy` learner/timestamp data;
- Assessment results;
- successful Course record.

### New data

#### `ProgressRequirement`

Stores Course Instance, source activity type/ID, required-or-optional classification, order, availability, alternative rules, and version.

#### `CourseProgressSummary`

Caches learner, Course Instance, required/optional values, next action, calculation version, and time.

#### Trusted completion adapter

Normalizes existing source data into unique, correctable occurrence IDs.

## 13. Success measures

- enrolled learners beginning meaningful work;
- reach rates at 25%, 50%, 75%, and 100% required progress;
- final-exam enrollment/participation/completion conversion;
- successful Course completion;
- optional activity participation;
- stage with greatest drop-off;
- frequency of source corrections or duplicate-event rejection.
