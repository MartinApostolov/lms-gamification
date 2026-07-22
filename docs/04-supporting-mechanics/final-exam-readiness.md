# Final Exam Readiness

> **Document status:** Rough functional outline grounded in the supplied LMS mock-up. Names, statuses, requirements, and technical structures remain provisional.

## 1. What

Final Exam Readiness shows whether a learner has completed the configured conditions needed to proceed to the final exam for a Course Instance.

The learner view provides:

- readiness status;
- required-condition checklist;
- optional preparation shown separately;
- the next missing action;
- actual exam enrollment and access-window information;
- known submission/result/pass state;
- attendance only when a future trusted source exists.

“Ready” means all configured readiness conditions are complete. It is not automatically identical to “Exam enrolled,” “Exam window open,” “Exam submitted,” “Exam passed,” or “Course completed.”

## 2. Current LMS grounding

The mock-up already stores:

- Course Instance exam references;
- assessment type: lesson assessment, quiz exam, or practical exam;
- exam enrollment;
- start/end date and time;
- quiz duration;
- price and payment-based access;
- exam URL and practical instruction file;
- practical submission and submission time;
- result start/completion time, score, grade, pass-score snapshot, and answer counts;
- successful Course completion after all attached exams are passed.

The mock-up does **not** store a separate verified exam-attendance event.

## 3. Why

The feature turns the final exam into a visible part of the Course journey. It answers:

- Am I enrolled for the exam?
- Is the exam available now?
- Which required learning or preparation condition is missing?
- Did I submit the practical work?
- Was my result recorded?
- Did I pass every required exam?
- What should I do next?

## 4. Status model

A layered model avoids collapsing different meanings into one label.

### Readiness status

| Status | Meaning |
|---|---|
| `NOT_CONFIGURED` | No readiness configuration exists |
| `IN_PROGRESS` | At least one required condition is incomplete |
| `READY` | All active required conditions are complete |

### Exam journey state

| State | Meaning |
|---|---|
| `NOT_ENROLLED` | Learner is not enrolled for the exam |
| `SCHEDULED` | Enrolled, but the exam window has not opened |
| `AVAILABLE` | Current time is inside the access window |
| `SUBMITTED` | Practical work or quiz result was submitted/recorded |
| `RESULT_PENDING` | A practical submission exists but no graded result exists |
| `PASSED` | Result meets the stored pass threshold |
| `NOT_PASSED` | Result exists below the pass threshold |
| `CLOSED_NO_RESULT` | Window closed and no result is available |

Courses may omit states that do not apply to their exam type.

## 5. Readiness conditions

Authorized staff may configure meaningful conditions such as:

- required Course Progress threshold;
- selected required lessons completed;
- required lesson assessment passed;
- exam enrollment confirmed;
- exam instructions acknowledged;
- prerequisite exam or practice assessment completed;
- another auditable manual condition.

Every condition requires a reliable source. The system must not infer completion from opening a page or the date passing.

Existing exam enrollment should normally be shown as an exam journey state. Whether it is also a readiness requirement is course configuration, not a universal rule.

## 6. Optional preparation

Optional preparation may include:

- extra practice assessment;
- Study Group revision session;
- optional Collaborative Challenge;
- additional resources;
- mock exam attempts beyond any required minimum.

It may affect optional Course Progress or achievements but does not block `READY`.

## 7. Next action

Examples:

```text
Next required action: Complete the prerequisite lesson assessment.
```

```text
You are ready. The practical exam opens on 15 June at 09:00.
```

```text
Submission received. Your practical result is pending.
```

The UI should link to the existing lesson, assessment, checkout/enrollment, exam, instruction, or submission page.

## 8. Events

Proposed readiness events:

- `EXAM_READINESS_UPDATED`;
- `EXAM_READY`;
- `EXAM_READY_REVOKED`.

Existing/adapted exam events:

- `EXAM_ENROLLED`;
- `EXAM_WINDOW_OPENED` and `EXAM_WINDOW_CLOSED` as scheduled state changes;
- `PRACTICAL_SUBMISSION_RECORDED`;
- `ASSESSMENT_COMPLETED`;
- `ASSESSMENT_PASSED`;
- `ASSESSMENT_NOT_PASSED`;
- `ASSESSMENT_RESULT_CORRECTED`;
- `COURSE_COMPLETED` after all Course Instance exams are passed.

Exam attendance remains unavailable and must not be emitted without a new trusted source.

## 9. Live and self-paced behavior

### Live

- scheduled lesson dates do not prove attendance;
- rescheduled/cancelled requirements use corrected dates;
- late learners see recovery or alternative paths;
- exam window, location/URL, and deadlines may be shown from current data.

### Self-paced

- readiness follows completed conditions rather than a fixed weekly pace;
- exam deadlines apply only when the exam is configured with them;
- inactivity does not revoke completed conditions;
- repeated attempts do not create multiple readiness credit for one condition.

## 10. Rules and edge cases

- Readiness belongs to learner + Course Instance.
- Required and optional conditions are visibly separate.
- All active required conditions are needed for `READY`.
- Corrections can return `READY` to `IN_PROGRESS` and must be audited.
- A practical submission does not imply a passing result.
- An exam enrollment does not imply attendance.
- An open/closed exam window does not imply activity.
- Course completion is reached only through the existing authoritative rule or its future replacement.
- Requirement changes must define treatment of learners already marked ready.
- Manual confirmation records actor, time, reason, and any evidence reference.
- Detailed readiness is private to learner and authorized staff.

## 11. Acceptance criteria

### AC1 — Existing exam data

Given the learner is enrolled in a configured exam,
when readiness is displayed,
then the exam type, relevant window, and enrollment state are shown without being counted as attendance.

### AC2 — Ready

Given all active required conditions are complete,
when readiness is calculated,
then status becomes `READY` once and `EXAM_READY` may be published.

### AC3 — Practical result pending

Given a valid practical submission exists
and no result exists,
when the exam journey is shown,
then the state is `RESULT_PENDING`, not `PASSED` or `EXAM_ATTENDED`.

### AC4 — Passed result

Given an exam result score meets its stored pass score,
when the result is evaluated,
then that exam state becomes `PASSED` and the associated readiness condition may complete once.

### AC5 — All-exam Course completion

Given every attached Course Instance exam has a passing result,
when the authoritative completion service runs,
then Course completion may be recorded and published separately from readiness.

### AC6 — No assumed attendance

Given the exam window closed
and no attendance source exists,
when the learner view is calculated,
then the system does not show `Exam Attended`.

### AC7 — Result correction

Given a previously passing result is corrected below the threshold,
when readiness and completion are recalculated,
then affected conditions and rewards receive auditable correction events.

## 12. Data and model extensions

### Existing data

- learner/Course Instance/Assessment enrollment;
- exam metadata and window;
- results, scores, pass thresholds, timestamps;
- practical submissions;
- successful Course records.

### New data

#### `ExamReadinessConfiguration`

Stores Course Instance, conditions, order, display text, alternatives, dates, manual-confirmation policy, and version.

#### `UserExamReadiness`

Stores learner, Course Instance, readiness status, completed/total counts, next action, and calculation version/time.

#### `ExamRequirementCompletion`

Stores one condition result with trusted source occurrence or manual confirmation and correction history.

## 13. Success measures

- learners viewing/beginning the checklist;
- learners reaching `READY`;
- exam enrollment and availability conversion;
- practical submission or quiz completion;
- exam pass rates;
- all-exam Course completion;
- most common missing readiness condition;
- change in final-exam participation once attendance data is available.
