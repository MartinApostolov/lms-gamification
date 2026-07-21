# Achievements and Badges

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Achievements and Badges recognizes meaningful learner accomplishments across courses, programs, exam preparation, optional learning, and validated community participation.

An **achievement** defines the accomplishment and the rule for earning it. A **badge** is its learner-facing visual representation.

Learners should be able to:

- view earned achievements;
- understand why and when each one was awarded;
- see the related course, course instance, program, or activity when applicable;
- choose whether eligible badges are visible to other learners.

Authorized course managers and administrators should be able to configure achievement definitions and audit awards. Achievements may be awarded automatically from trusted events or manually after authorized validation.

A small set of working examples is listed in **Initial Badges and XP Sources**. The exact achievement names, conditions, repeatability, and badge designs are not defined here and remain deferred until implementation.

## 2. Why

Course completion and the final exam may feel too distant to provide enough recognition throughout the learning journey. Achievements provide memorable evidence of meaningful accomplishments before and after course completion.

The feature supports:

- recognition of learning progress, preparation, and completion;
- optional exploration without making it mandatory;
- recognition of validated helpful participation;
- a personal history of learner accomplishments;
- different learner motivations without rewarding unnecessary website use.

Achievements must recognize meaningful outcomes rather than clicks, logins, time online, or unvalidated activity quantity.

## 3. How

### 3.1 Achievement definitions and scope

Each achievement definition should include:

- a unique identifier, name, and description;
- a badge visual reference;
- the trusted condition or event that awards it;
- its earning scope;
- whether it is one-time or repeatable;
- whether it is visible before being earned;
- whether it may be displayed publicly;
- whether it is enabled;
- its rule version.

Supported earning scopes may include:

| Scope | Meaning |
|---|---|
| Global | Earned once across the LMS |
| Per course | Earned once for a reusable course |
| Per course instance | Earned separately for each course delivery |
| Per program | Earned once for a program |
| Repeatable | Earned for separate valid occurrences under configured limits |

The future catalogue will select the correct scope for each individual achievement.

### 3.2 Trusted award sources

Achievements may use reliable events from the LMS or other gamification features, including:

- course progress and milestones;
- final-exam readiness, attendance, or completion;
- course or program completion;
- optional exploration activities;
- validated peer contributions;
- collaborative or competitive challenges;
- authorized manual confirmation.

This is a list of possible source categories, not the achievement catalogue.

An award source must identify the learner, achievement condition, related scope, source occurrence, and rule version.

### 3.3 Automatic and validated awards

An achievement may be:

- **automatic**, when a trusted system event proves the condition; or
- **validated**, when an authorized lecturer, moderator, or administrator confirms it.

A manual award must record who awarded it, when, why, and for which learner and scope.

### 3.4 Duplicate prevention and repeatability

A one-time achievement may be awarded only once within its configured scope. Reprocessing the same event must not create another achievement or another downstream reward event.

Repeatable achievements must be explicitly configured. Their definitions should specify what counts as a separate occurrence and any course, time-period, or lifetime limit.

Repeated page actions, repeated completion of the same activity, and raw message quantity must not create repeatable awards.

### 3.5 Learner display and privacy

The learner should have an achievement view showing earned badges and relevant details, for example:

```text
Achievement name
Description of the accomplishment
Earned: 21 July 2026
Related course: Course name
```

Unearned achievements may be visible, partially described, or hidden until earned. Hidden achievements must not contain undisclosed requirements for normal course completion or final-exam eligibility.

Learners should always see their own earned achievements. Detailed achievement history is private by default. Public or peer-visible badge display should require learner choice or a clearly communicated, privacy-controlled challenge rule.

The system may show a small in-LMS confirmation when an achievement is earned. Email, push, and exam reminder notifications are outside this feature.

### 3.6 Rule changes, corrections, and revocation

Each award should keep the version of the rule under which it was earned. Later rule changes should normally apply only to future awards.

A legitimately earned achievement should not disappear because a course threshold or achievement definition changes later.

An invalid award may be revoked when it resulted from incorrect data, fraud, or an incorrect manual decision. Revocation must preserve an audit record containing the reason, actor, and time.

Associated XP changes are handled by the XP feature.

## 4. Motivation types supported

- **Achievers — strong:** visible proof of progress, mastery, readiness, and completion.
- **Explorers — strong:** optional and discoverable achievements can recognize additional learning paths.
- **Socializers — medium:** validated contribution and collaboration achievements can recognize helpful participation.
- **Competitors — medium:** achievements may provide challenge recognition, but public comparison should remain optional.

## 5. Live-course behavior

- Achievements must use confirmed activity or attendance rather than a scheduled date simply passing.
- Cancelled or rescheduled lessons must use corrected source data before award evaluation.
- Late-enrolling learners may earn achievements when they satisfy the same configured conditions.
- Daily LMS visits must not be required unless they represent an approved meaningful learning activity.
- Achievements scoped per course instance may be earned again in a later delivery.

## 6. Self-paced-course behavior

- Learners may earn several achievements in one session after completing several valid requirements.
- Inactivity does not remove earned achievements.
- Reopening completed content does not create another award.
- Calendar-based achievements should be used only when the self-paced course defines a meaningful deadline or time-limited challenge.

## 7. Rules and edge cases

- No achievement is awarded for logging in, opening pages, remaining online, or repeatedly viewing content.
- Contribution achievements require trusted validation or another reliable quality signal.
- One source occurrence must not award the same achievement more than once.
- Optional achievements must not change required course progress or final-exam eligibility.
- Global achievements are not duplicated by repeated course enrollment.
- Disabled achievements cannot be awarded to new learners, but existing valid awards remain visible.
- A repeated course instance is separate only when the achievement scope allows it.
- Public achievement display must respect learner privacy settings.

## 8. Acceptance criteria

### AC1 — Automatic award

Given an enabled achievement has a trusted automatic condition
and a learner satisfies that condition,
when the source event is processed,
then the achievement is awarded with the correct learner, scope, source, rule version, and earned time.

### AC2 — Duplicate event

Given a learner already received a one-time achievement within its scope,
when the same event is processed again,
then no duplicate achievement or downstream reward event is created.

### AC3 — Per-course-instance scope

Given an achievement is scoped per course instance
and a learner earned it in an earlier instance,
when the learner satisfies the condition in a new instance,
then a separate award may be created for the new instance.

### AC4 — Global scope

Given an achievement is global and one-time
and the learner already earned it,
when the learner satisfies its condition in another course,
then it is not awarded again.

### AC5 — Manual validation

Given an achievement requires authorized validation,
when an authorized staff member confirms it,
then the award records the validator, time, reason, learner, and scope.

### AC6 — Optional achievement

Given a learner earns an optional achievement,
when the award is processed,
then required progress and final-exam readiness do not increase.

### AC7 — Invalid award correction

Given an achievement was awarded from incorrect source data,
when an authorized administrator revokes it,
then it is removed from the active earned-achievement display
and the award and revocation remain auditable.

### AC8 — Privacy

Given a learner has not chosen to display an eligible badge publicly,
when another learner views their profile,
then that badge is not shown.

## 9. Required LMS data

### Confirmed from the supplied models and completed feature requirements

- users and learner enrollment;
- courses, course instances, and programs;
- lesson completion and course completion;
- Course Progress values and events;
- Course Milestone records and events;
- Final Exam Readiness events when their source data exists.

### Missing or dependent on later features

- final-exam attendance and completion tracking;
- assignments, assessments, projects, and program-completion rules;
- discussions and contribution validation;
- study groups and collaborative challenge results;
- exploration and competitive challenge results;
- final badge artwork and the achievement catalogue.

Achievements that depend on missing data must not be enabled until a reliable source or authorized validation process exists.

## 10. Model extensions

The supplied LMS models should not be modified.

### `AchievementDefinition`

Stores the identifier, name, description, badge visual reference, award condition, scope, repeatability, visibility, enabled status, rule version, and optional course or program configuration.

### `UserAchievement`

Stores the learner, achievement definition and version, award scope, related course or program, earned time, source event, status, and public-visibility choice.

A unique rule should prevent duplicate one-time awards within their configured scope. Manual awards, corrections, and revocations must be auditable.

## 11. Success measure

The feature should support analysis of:

- percentage of active learners earning meaningful achievements;
- achievement earning rates at different course stages;
- progression to later milestones or the final exam after achievements are earned;
- participation in optional learning and validated helpful contributions;
- duplicate, revoked, or incorrectly awarded achievements;
- learner use of achievement visibility controls.

The goal is improved meaningful participation and completion, not maximizing the number of badges awarded.

## Related features

- [Course Progress](course-progress.md) supplies required and optional progress.
- [Course Milestones](course-milestones.md) supplies reliable course-checkpoint events.
- [Final Exam Readiness](final-exam-readiness.md) supplies exam-related statuses and events when supported by data.
- **Meaningful XP and Levels** may award or adjust XP in response to achievement events.
- Later social, exploration, collaborative, and competitive features may supply additional validated award sources.
- The initial examples are documented in **Initial Badges and XP Sources**; exact conditions, scope, repeatability, visibility, and artwork remain implementation decisions.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
