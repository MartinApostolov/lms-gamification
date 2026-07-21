# Peer Contribution Recognition

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Peer Contribution Recognition identifies and records learner contributions that have been validated as useful to other learners.

The feature is a recognition layer, not the communication system itself. It consumes trusted events from Course Q&A and Peer Help, Study Groups, Collaborative Challenges, or authorized staff validation.

Examples of potentially recognizable contributions include:

- an answer accepted as the solution to another learner’s question;
- a course-related resource approved as useful;
- a verified explanation or review contribution in a study group;
- meaningful work completed for a collaborative challenge;
- an exceptional helpful action manually confirmed by authorized staff.

A recognized contribution may generate XP, achievement progress, or a contribution statistic according to separate rules. Raw questions, answers, comments, reactions, and message counts do not automatically qualify.

## 2. Why

The project aims to encourage meaningful communication and cooperation between learners. Recognition gives learners a reason to help others while protecting the course community from spam and low-value posting.

The feature supports:

- peer-to-peer help outside scheduled lessons;
- stronger learning communities;
- recognition of Socializer-type learners;
- additional support for learners who might otherwise fall behind;
- trusted events for XP and Achievements and Badges.

The primary purpose is improved support and useful communication, not maximizing the quantity of posts.

## 3. How

### 3.1 Contribution types and validation

Each contribution-recognition rule should define:

- the contribution type;
- the trusted source and validation method;
- the recognition scope;
- whether it may repeat;
- applicable limits or cooldowns;
- downstream XP or achievement event type;
- correction and revocation behavior;
- enabled status and rule version.

Validation may come from:

- an accepted solution marked by the question author or authorized staff;
- lecturer, moderator, or administrator approval;
- completion of a clearly assigned part of a collaborative activity;
- a configured combination of peer feedback and moderator review.

Peer reactions alone should not award recognition in the first version because they are easy to manipulate.

### 3.2 Accepted solutions

An accepted solution is the clearest initial contribution type.

When a learner’s answer to another learner’s question is validly accepted, the system should create one contribution-recognition record for that answer and course instance.

The record should identify:

- contributor;
- question and answer;
- learner or staff member who accepted it;
- course instance;
- validation time;
- rule version;
- status.

The same answer cannot create repeated recognition when it is accepted, unaccepted, and accepted again without a new authorized decision under an applicable correction rule.

### 3.3 Limits and anti-farming controls

Repeatable contribution rewards may use configurable daily, weekly, course-instance, or lifetime limits.

Controls should include:

- no recognition for answering one’s own question;
- no self-validation;
- one active recognition per accepted answer;
- no recognition for duplicate, deleted, plagiarized, abusive, or off-topic content;
- audit of repeated mutual validation patterns;
- no direct reward for comments or reactions;
- moderator review and reversal capability;
- optional diminishing XP after repeated contributions while preserving the contribution count.

Limits should reduce farming without discouraging genuine help. A contribution may remain visible as helpful even when an XP cap prevents additional points.

### 3.4 Recognition status and correction

A contribution record may use statuses such as:

- Pending validation;
- Recognized;
- Rejected;
- Revoked.

If the accepted solution is removed, the source content is moderated, or the validation is found invalid, the recognition should be revoked. Revocation remains in the audit history and sends a correction event to XP and achievement systems.

A later rule change should normally affect future recognition only.

The feature may publish `CONTRIBUTION_RECOGNIZED` when validation succeeds and `CONTRIBUTION_REVOKED` when an active recognition is invalidated. XP and Achievements decide how those events affect rewards.

### 3.5 Learner and staff display

Learners should be able to see their own recognized contributions and why each was recognized.

A course-level display may show a restrained summary such as:

```text
Helpful contributions
3 accepted solutions
1 approved study resource
```

Detailed contribution history is private by default. Public contributor lists, leaderboards, or rankings require an opt-in competitive feature and appropriate privacy controls.

Authorized staff should be able to review pending, recognized, rejected, and revoked contributions.

## 4. Motivation types supported

- **Socializers — strong:** helpful interaction and support receive meaningful recognition.
- **Achievers — medium:** contribution records, XP, and achievements provide visible accomplishment.
- **Explorers — medium:** useful resources and alternative explanations may be recognized.
- **Competitors — low:** ranking contributors is outside this feature and should be optional.

## 5. Live-course behavior

- Contributions may occur between lessons and during exam preparation.
- Recognition is tied to actual helpful activity, not scheduled attendance alone.
- Late-enrolling learners may contribute and receive recognition after joining.
- Content related to cancelled or rescheduled lessons remains valid if it still helps learners.

## 6. Self-paced-course behavior

- Learners at different progress stages may help one another when the source discussion is properly contextualized.
- Contributions remain eligible regardless of whether they occur on a fixed schedule.
- Repeatedly posting the same answer across old questions should not create automatic recognition.
- Inactivity does not remove valid contribution history.

## 7. Rules and edge cases

- The question author cannot recognize their own answer to their own question.
- Staff may override an incorrect accepted solution, with an audit reason.
- Only one active accepted-solution recognition may exist per question.
- A contributor may receive recognition for separate valid questions, subject to configured limits.
- An XP cap does not require deleting the underlying recognized contribution.
- Contributions do not affect required course progress or exam eligibility unless the course explicitly defines a separate learning requirement.
- Removed or invalid content cannot remain an active recognition source.
- Public comparison is disabled by default.
- Staff manual recognition requires a reason and may not bypass anti-abuse rules without an auditable administrative override.

## 8. Acceptance criteria

### AC1 — Accepted solution recognition

Given a learner’s answer to another learner’s question is validly accepted,
when the accepted-solution event is processed,
then one Recognized contribution record is created for the answerer and course instance.

### AC2 — No reward for posting alone

Given a learner creates an answer or comment,
when it has not been validated by an eligible rule,
then no recognized contribution, XP award, or achievement event is created.

### AC3 — Duplicate prevention

Given an answer already has an active contribution-recognition record,
when the same validation event is processed again,
then no duplicate record or downstream reward event is created.

### AC4 — Self-validation blocked

Given a learner answered their own question,
when they attempt to validate that answer as a reward-eligible solution,
then no recognized contribution is created.

### AC5 — XP limit

Given a learner has reached the configured XP limit for repeatable accepted solutions,
when another valid answer is accepted,
then the contribution may still be recorded as recognized
but no additional XP is awarded beyond the configured limit.

### AC6 — Revocation

Given a recognized answer is removed or its validation is reversed,
when the correction is processed,
then the contribution becomes Revoked
and downstream XP or achievement systems receive a correction event.

### AC7 — Manual recognition

Given an authorized staff member validates an eligible exceptional contribution,
when they provide a reason and source reference,
then a contribution record is created with the validator and audit details.

### AC8 — Privacy

Given a learner has recognized contributions,
when another learner views standard course information,
then detailed contribution history is not shown unless a separate privacy-controlled feature enables it.

## 9. Required LMS data

### Confirmed or provided by related feature requirements

- users, courses, and course instances;
- Course Q&A questions, answers, accepted solutions, and correction events when implemented;
- XP and achievement integration events.

### Missing or dependent on later features

- study-group contribution records;
- collaborative challenge participation and validated individual work;
- resource approval workflow;
- moderation and abuse-monitoring signals;
- final recognition limits and XP values.

## 10. Model extensions

The supplied LMS models should not be modified.

### `ContributionRule`

Stores the source type, validation method, scope, repeatability, limits, downstream event, enabled status, and rule version.

### `ContributionRecognition`

Stores the contributor, rule, source reference, course or course instance, validator, validation time, status, reason, and timestamps.

### `ContributionAuditEvent`

Stores validation, rejection, revocation, restoration, and administrative override actions.

## 11. Success measure

Useful indicators include:

- percentage of course questions receiving accepted solutions;
- number and percentage of learners giving at least one recognized contribution;
- distribution of recognition across learners rather than concentration in a few accounts;
- repeat engagement of learners who receive peer help;
- relationship between helpful participation, retention, exam readiness, and course completion;
- rejected, revoked, capped, and abuse-related recognition rates.

Raw message count is not a success measure.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
