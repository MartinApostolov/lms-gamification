# Course Progress

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](../02-planning-and-standards/document-status-and-theming.md).

## 1. What

Course Progress shows each learner how much of a particular course delivery they have completed and what meaningful activity they should complete next.

Progress belongs to a learner's enrollment in a specific course instance:

```text
User + CourseInstance
```

The learner view should show:

- required course progress from 0% to 100%;
- optional activity progress from 0% to 100%;
- combined progress from 0 to 200 points;
- completed and remaining activities;
- the next recommended activity;
- whether the required course work is complete.

Example:

```text
Required progress: 75 / 100
Optional progress: 40 / 100
Total progress: 115 / 200

Next required activity: Complete Lesson 10
```

The combined value is shown as points out of 200, not as “200% course completion.” The learner completes the course requirements when the required part reaches 100%, subject to the LMS course-completion rules. Optional progress does not block completion.

Authorized lecturers and course managers should be able to view progress for learners in their course instances. Administrators should be able to audit progress calculations and configure system defaults.

## 2. Why

The main business problem is the large drop-off between enrollment and final-exam participation. Learners may stop participating because the end goal feels distant, completed work is not visible, or the next step is unclear.

Course Progress breaks the course into understandable amounts of work and makes the next action visible without encouraging unnecessary website use.

The feature supports the goals of:

- increasing the number of enrolled learners who start the course;
- retaining more learners through the middle and later course stages;
- helping learners recover after falling behind;
- supporting preparation for the final exam;
- increasing course completion.

## 3. How

### 3.1 Required progress

Required progress represents activities that are necessary for normal course completion.

For the initial implementation, progress can be calculated from required lesson completion:

```text
Unique required lessons completed
--------------------------------- × 100
Total required lessons
```

Example:

```text
9 completed required lessons / 12 required lessons = 75%
```

Only meaningful, completed activities may increase progress. Opening a lesson, logging in, remaining online, or repeatedly viewing completed content must not increase it.

### 3.2 Optional progress

Optional progress represents additional course-related activities that are not necessary for normal completion or final-exam eligibility unless explicitly configured otherwise.

It is calculated separately:

```text
Unique optional activities completed
------------------------------------ × 100
Total optional activities
```

Optional activities may include extra practice, additional resources, alternative exercises, or exploration challenges.

When a course has no optional activities, the optional value and combined total may be hidden rather than displayed as 0 / 100.

### 3.3 Combined progress

The combined value is the sum of the required and optional percentages expressed as points:

```text
Required progress points + Optional progress points = Total points out of 200
```

Example:

```text
Required: 75 / 100
Optional: 40 / 100
Total:    115 / 200
```

The combined value provides an additional goal for learners who want to complete everything. It must not replace the required course-completion value.

### 3.4 Next recommended activity

The system should show at least one meaningful next action whenever possible.

Priority should normally be:

1. incomplete required activities;
2. time-sensitive required activities;
3. final-exam readiness requirements;
4. optional activities.

Examples:

```text
Next required activity: Complete Lesson 10
```

```text
All required activities are complete.
Optional activity: Try the advanced practice task.
```

### 3.5 Recalculation

Progress must be recalculated when relevant LMS data or course requirements change.

Examples include:

- a lesson is completed;
- an incorrect completion is removed;
- a lesson changes between required and optional;
- a required activity is added or removed;
- a learner changes course instance.

Course Progress may publish proposed events such as:

- `REQUIRED_PROGRESS_UPDATED`;
- `OPTIONAL_PROGRESS_UPDATED`;
- `COURSE_PROGRESS_RECALCULATED`.

The existing LMS or another configured source remains authoritative for the underlying activity completion and final course-completion record.

The LMS completion records remain the source of truth. A gamification progress record may cache the calculated result for display and reporting.

## 4. Motivation types supported

- **Achievers — strong:** clear required progress, visible completion, and a total goal of 200 points.
- **Explorers — strong:** optional progress recognizes additional learning without making it mandatory.
- **Socializers — low:** this feature does not directly reward communication.
- **Competitors — low:** progress is personal by default and is not publicly ranked.

## 5. Live-course behavior

For live courses, progress should follow meaningful course requirements rather than daily website activity.

- Scheduled lesson dates do not automatically prove attendance or completion.
- A learner is not penalized for not visiting the LMS between scheduled lessons.
- Cancelled lessons should not count against the learner.
- Rescheduled lessons should use the updated schedule.
- Late-enrolling learners should see missed and remaining requirements without receiving automatic completion for earlier lessons.
- Attendance may affect progress only when reliable attendance data exists.

## 6. Self-paced-course behavior

For self-paced courses:

- progress is based on completed required and optional activities;
- the learner may complete several activities in one session;
- inactivity does not reduce completed progress;
- reopening completed content does not create more progress;
- fixed calendar activity is not required unless the course explicitly defines deadlines.

## 7. Rules and edge cases

- Each activity may contribute only once to the relevant progress value.
- Required and optional progress must each remain between 0 and 100.
- Total progress must remain between 0 and 200.
- Optional completion must not increase required progress.
- Progress from one course instance must not automatically transfer to another instance.
- A correction may reduce the current displayed progress, and the correction must be auditable.
- Significant course changes should not silently make already-completed learners incomplete unless an administrator explicitly allows it.
- Detailed learner progress is private by default and visible only to the learner and authorized staff.

## 8. Acceptance criteria

### AC1 — Initial progress

Given a learner is enrolled in a course instance and has completed no activities,
when progress is calculated,
then required progress is 0%
and the first required activity is shown as the next action.

### AC2 — Required progress calculation

Given a course has 12 required lessons
and the learner has completed 9 unique required lessons,
when progress is calculated,
then required progress is 75%.

### AC3 — Optional progress calculation

Given a course has 10 optional activities
and the learner has completed 4 unique optional activities,
when progress is calculated,
then optional progress is 40%.

### AC4 — Combined progress

Given required progress is 75%
and optional progress is 40%,
when total progress is displayed,
then the system shows 115 / 200 points.

### AC5 — Optional work does not complete the course

Given required progress is 80%
and optional progress is 100%,
when progress is evaluated,
then the learner is not marked complete based only on the combined 180 / 200 points.

### AC6 — Duplicate completion

Given an activity is already recorded as complete,
when the same completion event is processed again,
then neither required nor optional progress increases.

### AC7 — Corrected source data

Given a required lesson was marked complete incorrectly,
when an authorized correction removes the completion,
then required and total progress are recalculated
and the correction is recorded for auditing.

### AC8 — Separate course instance

Given a learner completed an earlier instance of a course,
when the learner enrolls in a new instance,
then the new enrollment starts with separate progress unless an explicit transfer rule is applied.

## 9. Required LMS data

### Confirmed from the supplied models

- learner enrollment in a course instance;
- live or self-paced course type;
- lesson completion with user and timestamp;
- successful course completion.

### Missing or requiring confirmation

- which lessons are required or optional;
- non-lesson activity completion;
- assignment and assessment results;
- attendance data;
- the exact LMS rule for successful course completion.

## 10. Model extensions

The supplied LMS models should not be modified.

A small extension may include:

### `ProgressRequirement`

Defines whether an existing lesson or another activity is required or optional and its display order.

### `CourseProgressSummary`

Stores or caches the learner's required progress, optional progress, total points, next activity, calculation time, user, and course instance.

Existing LMS completion records remain the source of truth.

## 11. Success measure

The feature should be evaluated through:

- percentage of enrolled learners who begin the course;
- percentage reaching 25%, 50%, 75%, and 100% required progress;
- percentage participating in optional learning activities;
- change in final-exam participation;
- change in successful course completion;
- the course stage with the largest learner drop-off.

## Related features

- [Course Milestones](course-milestones.md) recognizes important points calculated from course progress.
- [Final Exam Readiness](final-exam-readiness.md) tracks the requirements that must be completed before the final exam.

See [Gamification Event Matrix](../06-integrations/gamification-event-matrix.md) for proposed event ownership and integrations.
