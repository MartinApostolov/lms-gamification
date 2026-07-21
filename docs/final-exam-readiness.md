# Final Exam Readiness

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Final Exam Readiness shows whether a learner has completed the configured requirements needed to proceed to the final exam for a particular course instance.

The feature provides:

- a clear readiness status;
- a checklist of required exam conditions;
- optional preparation activities shown separately;
- the remaining action needed before the learner is ready;
- confirmed exam attendance or completion when those events are available.

Example:

```text
Final Exam Readiness: 3 of 4 required conditions complete

✓ Required lessons completed
✓ Exam instructions reviewed
✓ Practice assessment completed
○ Required project not submitted

Next step: Submit the required project
```

For this feature, **Ready** means that all configured required readiness conditions are complete. Optional preparation may improve confidence but must not block readiness.

## 2. Why

The largest business problem is the drop-off between course enrollment and final-exam participation. Learners may not know:

- whether they are eligible or ready;
- which requirements remain;
- where to find exam information;
- whether missing work can be recovered;
- what action should be completed next.

The feature keeps the final exam visible as part of the course journey and turns preparation into a clear set of achievable requirements.

## 3. How

### 3.1 Readiness statuses

The feature should support these statuses:

| Status | Meaning |
|---|---|
| Not Available | Readiness tracking or exam information is not yet available |
| In Progress | At least one required readiness condition remains incomplete |
| Ready | All required readiness conditions are complete |
| Exam Attended | Attendance has been confirmed |
| Exam Completed | Completion has been confirmed, regardless of whether scoring is stored separately |

A course may omit statuses that cannot be supported by its available data.

### 3.2 Readiness requirements

Course managers should be able to configure meaningful required conditions, such as:

- completing required lessons;
- submitting a required project;
- passing a required assessment;
- reviewing exam instructions;
- confirming intention to attend;
- satisfying a confirmed attendance requirement;
- completing another course-specific eligibility condition.

Each requirement must have a reliable completion source. A requirement must not be configured when the system cannot determine whether it was completed, unless an authorized staff member can confirm it manually.

### 3.3 Optional preparation

Optional preparation is displayed separately from readiness requirements.

Examples include:

- extra practice tasks;
- optional study-group participation;
- additional revision resources;
- mock exam attempts beyond the required amount.

Optional preparation may contribute to Course Progress optional points or separate achievements, but it does not prevent the learner from becoming Ready.

### 3.4 Next action

When the learner is not Ready, the feature should identify at least one incomplete required condition.

When all conditions are complete, it should show the next available exam action, such as:

```text
You are ready for the final exam.
Review the exam date and location.
```

or:

```text
You are ready for the final exam.
Registration opens on 15 June.
```

### 3.5 Configuration

Authorized course managers may configure:

- required readiness conditions;
- optional preparation activities;
- condition order and learner-facing text;
- availability dates and deadlines;
- recovery or alternative conditions;
- which statuses are supported by the course;
- whether manual staff confirmation is allowed.

### 3.6 Exam-related events and notifications

This feature may publish readiness events such as:

- `EXAM_READINESS_UPDATED`;
- `EXAM_READY`;
- `EXAM_READY_REVOKED` after a correction.

It may consume or expose trusted exam-system events such as `EXAM_REGISTRATION_AVAILABLE`, `EXAM_ATTENDANCE_CONFIRMED`, and `EXAM_COMPLETED`. Attendance and completion must come from a reliable exam, attendance, assessment, or auditable manual source; they must not be inferred from the exam date passing.

Exam dates, registration deadlines, missing critical requirements, and similar exam information may justify notifications. Notification delivery, channels, frequency, and user preferences should be defined in a separate notification feature.

Ordinary course milestones do not need notifications.

## 4. Motivation types supported

- **Achievers — strong:** a concrete checklist and Ready status provide a clear goal.
- **Explorers — medium:** optional preparation provides additional paths without changing eligibility.
- **Socializers — medium:** optional group preparation may support readiness, but personal readiness must not depend entirely on other learners.
- **Competitors — low:** readiness is personal and not publicly ranked.

## 5. Live-course behavior

- Readiness may consider scheduled required lessons and confirmed attendance when attendance data exists.
- A lesson date passing does not prove attendance.
- Cancelled or rescheduled sessions must use the corrected schedule.
- Late-enrolling learners should see missed requirements, available recovery paths, and whether readiness is still achievable.
- Exam dates, locations, registration windows, and deadlines may be shown when supplied by the LMS or another trusted source.

## 6. Self-paced-course behavior

- Readiness should depend on completed requirements rather than a fixed pace.
- Inactivity does not remove completed conditions.
- Learners may complete several conditions in one session.
- Deadlines should apply only when explicitly configured for the course or exam.
- Repeating an already completed requirement does not increase readiness progress.

## 7. Rules and edge cases

- Readiness belongs to a learner and a specific course instance.
- Required and optional preparation must be visibly separated.
- Ready is reached only when every active required condition is complete.
- Duplicate source events must not create duplicate completion records.
- A corrected source record may return the status from Ready to In Progress, and the correction must be auditable.
- Requirements added after learners are already Ready should not silently remove readiness unless an administrator explicitly approves how the change applies.
- A repeated course instance has separate readiness.
- Manual confirmations must record who made the decision and when.
- Learners may view only their own detailed readiness data unless authorized otherwise.
- Exam attendance must not be inferred from enrollment, registration, or the exam date passing.

## 8. Acceptance criteria

### AC1 — Initial readiness

Given a course has configured final-exam requirements
and the learner has completed none of them,
when readiness is displayed,
then the status is In Progress
and the first incomplete required condition is shown.

### AC2 — Partial readiness

Given a course has four required readiness conditions
and the learner has completed three,
when readiness is displayed,
then the system shows 3 of 4 complete
and identifies the remaining condition.

### AC3 — Ready status

Given all active required readiness conditions are complete,
when readiness is evaluated,
then the learner's status becomes Ready once
and an EXAM_READY event may be published.

### AC4 — Optional preparation

Given the learner has not completed an optional preparation activity,
when all required readiness conditions are complete,
then the learner may still become Ready.

### AC5 — No assumed attendance

Given the exam date has passed
and no confirmed attendance record exists,
when readiness is evaluated,
then the learner is not marked Exam Attended.

### AC6 — Duplicate completion event

Given a readiness condition is already complete,
when the same source event is processed again,
then the completed-condition count does not increase.

### AC7 — Corrected requirement

Given the learner is Ready
and an authorized correction removes completion of a required condition,
when readiness is recalculated,
then the status returns to In Progress
and the correction is recorded for auditing.

### AC8 — Exam notification integration

Given an exam-related event is published,
when a separate notification feature consumes the event,
then notification behavior may be applied without being implemented inside Final Exam Readiness.

## 9. Required LMS data

### Confirmed from the supplied models

- learner enrollment in a course instance;
- lesson completion with timestamps;
- course-instance exam references;
- live or self-paced course type;
- successful course completion.

### Missing or not confirmed

- final-exam attendance;
- final-exam completion or score;
- assignment or project submission;
- assessment attempt and pass/fail result;
- review of exam instructions;
- intention-to-attend confirmation;
- reliable live-session attendance;
- exact exam eligibility rules.

These missing events require new tracking, integration with another LMS service, or an auditable manual confirmation.

## 10. Model extensions

### `ExamReadinessConfiguration`

Defines the readiness conditions, optional preparation activities, ordering, availability, deadlines, recovery rules, and course-instance scope.

### `UserExamReadiness`

Stores the learner, course instance, current status, completed required-condition count, total required-condition count, next required action, and last calculation time.

### `ExamRequirementCompletion`

Stores completion of an individual condition, including its source event or manual confirmation and audit information.

## 11. Success measure

The feature should be evaluated through:

- percentage of enrolled learners who open or begin the readiness checklist;
- percentage who reach Ready status;
- conversion from Ready to Exam Attended;
- conversion from Exam Attended to Exam Completed;
- most common incomplete requirement;
- change in overall final-exam participation;
- change in course completion after the feature is introduced.

## Related features

- [Course Progress](course-progress.md) provides required and optional learning progress that may satisfy readiness conditions.
- [Course Milestones](course-milestones.md) may recognize the Ready, Exam Attended, or Exam Completed events, but does not define the readiness requirements.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
