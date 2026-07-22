# Course Milestones

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](../02-planning-and-standards/document-status-and-theming.md).

## 1. What

Course Milestones records and displays meaningful checkpoints that a learner reaches during a specific course instance.

Milestones recognize progress without changing the progress calculation itself. They may later be used by achievements, badges, XP, or analytics, but those rewards are separate features.

Default milestone examples include:

| Milestone | Default condition |
|---|---|
| Course Started | First required activity is completed |
| 25% Required Progress | Required progress reaches at least 25% |
| Halfway | Required progress reaches at least 50% |
| 75% Required Progress | Required progress reaches at least 75% |
| Required Work Complete | Required progress reaches 100% |
| Optional Explorer | Optional progress reaches a configured threshold |
| All Activities Complete | Required and optional progress both reach 100%, when optional activities exist |
| Course Completed | The LMS records successful course completion |

Course managers should be able to enable, disable, rename, or change thresholds for course-specific milestones.

Ordinary milestone notifications are not part of this feature. Learners see milestones in the course progress interface. Final-exam reminders and similar messages belong to the exam or notification feature.

## 2. Why

A complete course may feel too distant to learners. Milestones divide the journey into smaller accomplishments and recognize progress before the final result.

The feature supports:

- continued motivation through the course;
- recognition of meaningful work;
- clearer movement toward completion;
- analysis of where learners stop progressing;
- reliable triggers for later gamification rewards.

## 3. How

### 3.1 Milestone source

A milestone may be triggered by:

- a required-progress threshold;
- an optional-progress threshold;
- a combined 200-point condition;
- a confirmed LMS event such as course completion;
- another configured meaningful condition.

Milestones must not be triggered by logins, page views, time online, or repeated completion of the same activity.

### 3.2 Milestone ownership

A reached milestone belongs to:

```text
User + CourseInstance + MilestoneDefinition
```

This keeps milestone history separate for repeated deliveries of the same course.

### 3.3 Award once

A learner may reach the same milestone only once for the same course instance.

Processing the same LMS event more than once must not create duplicate records or duplicate reward events.

### 3.4 Crossing multiple thresholds

One recalculation may cause the learner to cross several milestones.

Example:

```text
Previous required progress: 20%
Corrected required progress: 55%
```

The learner reaches both the 25% and Halfway milestones. Another learner action is not required between them.

### 3.5 Configuration

Authorized course managers may configure:

- milestone name and description;
- required, optional, combined, or event-based type;
- percentage or point threshold;
- whether the milestone is enabled;
- whether it is visible to learners;
- whether it applies to live courses, self-paced courses, or both;
- whether a system default is overridden for a course or course instance.

Configuration changes should be auditable.

### 3.6 Corrections

When source data is corrected, the learner's current progress is recalculated.

A milestone already reached should remain in the audit history. Its status may be marked as corrected or no longer currently satisfied, but the same milestone must not generate another reward if the learner later crosses the threshold again.

Whether XP or a badge is removed is decided by the XP or achievement feature, not by Course Milestones.

### 3.7 Events for other features

The feature should publish a generic `MILESTONE_REACHED` event. Its payload identifies the milestone definition or type, for example Course Started, Halfway, Required Work Complete, or All Activities Complete.

Course Milestones may consume source events such as `COURSE_COMPLETED`, but the existing LMS course-completion record remains the source of truth for course completion.

The milestone event must include enough information to prevent duplicate downstream rewards.

## 4. Motivation types supported

- **Achievers — strong:** milestones recognize progress, completion, and mastery.
- **Explorers — medium:** optional milestones recognize additional learning paths.
- **Socializers — low:** personal milestones do not depend on other learners.
- **Competitors — low:** no public comparison is included by default.

## 5. Live-course behavior

- Milestones are based on confirmed progress or events, not merely on scheduled dates passing.
- Cancelled or rescheduled lessons should affect progress before milestone evaluation.
- Late-enrolling learners may earn milestones when they satisfy the same meaningful conditions.
- Attendance milestones require reliable attendance data and must not infer attendance from enrollment.

## 6. Self-paced-course behavior

- Learners may reach several milestones in one learning session.
- No milestone is lost because the learner takes a break.
- Reopening completed activities does not create additional milestones.
- Calendar-based milestones should be disabled unless the self-paced course explicitly uses dates.

## 7. Rules and edge cases

- A unique rule must prevent duplicate user milestone records.
- Threshold milestones are reached when the value is equal to or greater than the configured threshold.
- Required and optional milestones must identify which progress scale they use.
- A 100% optional milestone must not imply required course completion.
- “All Activities Complete” is available only when the course contains optional activities.
- Milestones for a repeated course instance may be earned again because the enrollment is separate.
- Hidden milestones may be stored without being shown to learners.
- Learners may view only their own personal milestone history unless authorized otherwise.
- Ordinary milestones do not send notifications.

## 8. Acceptance criteria

### AC1 — Course started

Given a learner has not started the course,
when the learner completes the first required activity,
then the Course Started milestone is recorded once.

### AC2 — Required threshold

Given the learner has not reached the Halfway milestone,
when required progress reaches or exceeds 50%,
then the Halfway milestone is recorded once.

### AC3 — Optional threshold

Given an optional milestone is configured at 50%,
when optional progress reaches 50%,
then the optional milestone is recorded
without changing required progress or course-completion status.

### AC4 — Multiple milestones

Given required progress changes from 20% to 55%,
when milestone evaluation runs,
then both the 25% and Halfway milestones are recorded.

### AC5 — Duplicate processing

Given a milestone has already been recorded,
when the same source event is processed again,
then no duplicate milestone or downstream reward event is created.

### AC6 — All activities complete

Given a course contains optional activities,
when required progress reaches 100%
and optional progress reaches 100%,
then the All Activities Complete milestone is recorded.

### AC7 — Correction

Given a learner previously reached a threshold
and source data is later corrected below that threshold,
when milestones are recalculated,
then the original record remains auditable
and crossing the same threshold again does not generate a duplicate reward event.

### AC8 — No milestone notification

Given a learner reaches an ordinary course milestone,
when the milestone is recorded,
then the system does not require a notification to be sent.

## 9. Required LMS data

### Confirmed from the supplied models

- learner and course-instance enrollment;
- lesson completion with timestamps;
- course completion;
- live or self-paced course type.

### Missing or requiring configuration

- required and optional activity classification;
- reliable attendance;
- assessment outcomes;
- final-exam attendance and completion;
- course-specific milestone definitions.

## 10. Model extensions

### `MilestoneDefinition`

Stores the name, description, type, threshold or condition, visibility, enabled status, and course or course-instance override.

### `UserMilestone`

Stores the learner, course instance, milestone definition, achieved time, source event, and correction status.

A unique constraint should cover the learner, course instance, and milestone definition.

## 11. Success measure

The feature should support analysis of:

- percentage of enrolled learners reaching each required milestone;
- percentage reaching optional milestones;
- average time between milestones;
- the milestone after which the largest drop-off occurs;
- changes in final-exam participation and course completion after milestone introduction.

## Related features

- [Course Progress](course-progress.md) supplies the required and optional progress values used by threshold milestones.
- [Final Exam Readiness](final-exam-readiness.md) defines exam-specific requirements and statuses rather than treating readiness as a normal percentage milestone.

See [Gamification Event Matrix](../06-integrations/gamification-event-matrix.md) for proposed event ownership and integrations.
