# Collaborative Challenges

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Collaborative Challenges gives learners a shared, time-bounded or course-stage-based learning goal that requires contributions from more than one participant.

A challenge may be completed by:

- a study group;
- a temporary team created for the challenge;
- the whole course instance when the goal is genuinely collective.

Examples may later include completing an exam-preparation set, producing a shared resource collection, reviewing practice questions, or reaching a group learning milestone.

This document defines the challenge framework, not the final list of challenges. Individual goals, requirements, XP amounts, and achievements should be maintained later in a **Challenge Catalogue**.

Collaborative Challenges is separate from Study Groups. A group is an ongoing membership structure; a challenge is a defined activity with eligibility, progress, completion, and reward rules.

## 2. Why

Shared goals give learners a structured reason to communicate and prepare together. They can help learners remain engaged, support one another, and make progress toward the final exam without relying on public individual rankings.

The feature supports:

- meaningful cooperation;
- team accountability;
- exam preparation;
- recognition of different forms of contribution;
- Socializers, Achievers, and learners who enjoy team-based competition.

A challenge must be connected to a real learning or support outcome. It must not reward teams for logins, time online, message volume, or repeated low-value activity.

## 3. How

### 3.1 Challenge definition

Each challenge definition should include:

- name, description, and learning purpose;
- eligible course or course instance;
- eligible group or team type;
- start, end, or course-stage availability;
- trusted progress requirements;
- collective completion condition;
- minimum individual contribution for personal rewards where applicable;
- reward events;
- joining and late-entry rules;
- visibility, enabled status, and rule version.

### 3.2 Cooperative progress

Challenge progress should come from trusted learning or contribution events, such as:

- completing assigned preparation activities;
- contributing a validated answer or resource;
- completing assigned parts of a group task;
- confirmed participation in a structured review activity;
- satisfying a group milestone based on verified member actions.

The interface should show:

- the shared goal;
- current team progress;
- remaining requirements;
- deadline or availability period;
- each learner’s own eligible contribution status.

### 3.3 Team completion and individual eligibility

The system should distinguish:

1. **team completion** — whether the shared goal was reached; and
2. **individual reward eligibility** — whether a particular learner contributed enough to receive the configured personal reward.

This prevents one highly active learner from completing the challenge while inactive members receive identical recognition merely for membership.

A challenge may allow a team-level badge or record for all members while requiring a minimum verified contribution for personal XP or an individual achievement.

### 3.4 Teams and membership

A challenge may use an existing study group or create a temporary team.

Joining a challenge or team does not award XP. Team membership should be fixed or controlled after the challenge begins when changes could create unfair rewards.

Authorized staff should be able to replace a learner who withdraws, correct membership, or cancel a team with an audit reason.

### 3.5 Completion and reward events

When the completion condition is satisfied, the system should generate trusted events such as:

- `COLLABORATIVE_CHALLENGE_COMPLETED` for the team;
- `COLLABORATIVE_CONTRIBUTION_CONFIRMED` for eligible learners;
- `COLLABORATIVE_CONTRIBUTION_REVOKED` when a counted contribution is invalidated.

XP and achievement amounts, awards, and reversals are handled by their own rule catalogues.

### 3.6 Challenge changes and cancellation

Material rule changes after a challenge starts should normally require a new challenge version or apply only to future instances.

If a challenge is cancelled:

- no unearned completion rewards are issued;
- valid contribution recognition already earned may remain when appropriate;
- the cancellation reason is recorded;
- learners see that the challenge was cancelled rather than failed.

## 4. Motivation types supported

- **Socializers — strong:** structured cooperation and shared goals.
- **Achievers — strong:** clear requirements, progress, and completion recognition.
- **Competitors — medium:** teams may later compare performance in opt-in formats, but competition is not required.
- **Explorers — medium:** some challenges may allow different contribution paths or shared resource discovery.

## 5. Live-course behavior

- Challenges may align with lesson blocks, revision periods, or the final exam.
- Scheduled dates may control availability but do not prove participation.
- Cancelled or rescheduled lessons should update challenge timing when relevant.
- Late-enrolling learners may join only according to the challenge’s fairness rules and cannot receive credit for earlier team activity they did not contribute to.
- Learners should not be required to visit daily unless the challenge itself contains a meaningful daily learning requirement.

## 6. Self-paced-course behavior

- Challenges may use broader availability windows or progress-stage eligibility.
- Teams should avoid requiring all members to be on the same exact lesson unless that is the purpose.
- A learner taking a break receives no penalty beyond missing an explicitly communicated challenge period.
- Progress events remain tied to verified completion, not time online.

## 7. Rules and edge cases

- Joining a challenge or team creates no reward.
- Team completion alone does not guarantee every member a personal reward.
- Minimum individual contribution must be visible before participation begins.
- The same source event cannot count repeatedly unless the challenge explicitly allows distinct occurrences.
- A learner cannot validate their own contribution where validation is required.
- Challenge progress does not alter required course progress unless the underlying activity is independently a course requirement.
- Optional collaborative challenges cannot become hidden requirements for course completion or exam eligibility.
- Team size changes after the start must be auditable.
- Corrected or removed source activity must recalculate challenge progress and personal eligibility.
- Public team comparison requires a separate opt-in competitive rule.

## 8. Acceptance criteria

### AC1 — Start a challenge

Given an enabled challenge definition and eligible team,
when the challenge availability period begins,
then the team can view the shared goal, requirements, progress, deadline, and individual eligibility rule.

### AC2 — Record valid contribution

Given a learner performs a trusted eligible activity,
when the source event is processed,
then team progress and the learner’s contribution status are updated once.

### AC3 — Duplicate event

Given a source occurrence already counted toward the challenge,
when the same event is processed again,
then challenge progress does not increase again.

### AC4 — Team completion

Given the team satisfies all collective challenge requirements,
when progress is calculated,
then the challenge becomes Completed
and one team-completion event is generated.

### AC5 — Individual minimum

Given the team completes the challenge
but a member did not satisfy the visible minimum individual contribution,
when rewards are evaluated,
then that member does not receive the configured personal reward solely because they were a member.

### AC6 — Eligible individual reward

Given the team completes the challenge
and a learner satisfies the minimum individual contribution,
when rewards are evaluated,
then one eligible-contribution event is generated for that learner.

### AC7 — Corrected contribution

Given a counted contribution is later invalidated,
when challenge progress is recalculated,
then team progress and individual eligibility are corrected
and any affected downstream reward receives a correction event.

### AC8 — Cancellation

Given authorized staff cancels an active challenge,
when the cancellation is processed,
then the status becomes Cancelled,
no unearned completion rewards are generated,
and the reason is visible and auditable.

## 9. Required LMS data

### Confirmed or provided by related feature requirements

- users, courses, course instances, and enrollment;
- Course Progress and Milestone events;
- Study Group membership when implemented;
- Q&A and Peer Contribution events when implemented;
- XP and Achievement integrations.

### Missing or challenge-specific

- challenge definitions and instances;
- temporary team membership;
- verified group-task and preparation activity completion;
- individual contribution tracking;
- final challenge catalogue and reward rules.

## 10. Model extensions

The supplied LMS models should not be modified.

### `CollaborativeChallengeDefinition`

Stores the learning purpose, eligibility, availability, requirements, contribution rules, reward event types, enabled status, and rule version.

### `CollaborativeChallengeInstance`

Stores the definition version, course instance, participating group or team, dates, status, and current progress.

### `ChallengeTeamMembership`

Stores temporary team membership where an existing study group is not used.

### `ChallengeContribution`

Stores the learner, trusted source occurrence, contribution value or requirement, validation status, and timestamps.

### `ChallengeAuditEvent`

Stores rule changes, membership corrections, cancellation, progress corrections, and staff actions.

## 11. Success measure

Useful indicators include:

- challenge participation and completion rates;
- percentage of participants satisfying minimum individual contribution;
- distribution of work across team members;
- movement toward course milestones, exam readiness, exam attendance, and completion;
- contribution corrections, inactive membership, and challenge cancellation rates;
- learner feedback on cooperation and fairness.

Message volume, team membership, and time online are not success measures by themselves.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
