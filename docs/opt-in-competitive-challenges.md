# Opt-in Competitive Challenges

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Opt-in Competitive Challenges give learners a voluntary way to compare performance through fair, limited, and course-related contests.

Possible formats include personal-best challenges, small-group rankings, team contests, milestone races, or periodic scoreboards. In a themed interface, they could appear as tournaments, trials, friendly contests, or party competitions.

This document defines the competition framework. It does not define the final competitions, scoring values, XP amounts, achievements, or visual presentation. Those should be maintained later in a **Challenge Catalogue**.

## 2. Why

Some learners are motivated by comparison, mastery, status, and testing their performance against others or against their own previous results.

Used carefully, competition can:

- create an additional voluntary goal;
- make revision or practice more engaging;
- encourage learners to improve their own result;
- support friendly team interaction;
- provide short, resettable moments of challenge without creating a permanent hierarchy.

Competition must not become the default measure of learner worth or discourage learners who join late, progress more slowly, or prefer not to participate.

## 3. How

### 3.1 Explicit opt-in

Learners must actively join a competitive challenge before their name, score, rank, or team participation is shown to other participants.

Not joining must not reduce:

- required or optional course progress;
- final-exam eligibility;
- access to normal learning content;
- standard course completion;
- ordinary XP or achievements earned outside the competition.

Learners should be able to leave where fairness permits. The rules must explain whether leaving hides future participation only or also removes the learner from the current ranking.

### 3.2 Challenge definition

A competitive challenge should define:

- title, description, and learning purpose;
- individual, personal-best, study-group, or team format;
- eligible course, course instance, stage, or group;
- registration and active periods;
- trusted scoring events and scoring rules;
- comparison group and fairness rules;
- tie handling;
- minimum participation or completion conditions;
- leaderboard visibility and privacy options;
- reset, finalization, cancellation, and correction behavior;
- reward event types;
- enabled status and rule version.

### 3.3 Possible formats

#### Personal best

The learner competes against their own previous verified result. This may be offered without showing any public ranking.

#### Small cohort ranking

Learners at a similar course stage or with a similar joining period are compared within a limited group.

#### Study-group or team contest

Groups compete using verified collective activity. Individual reward eligibility may still require a minimum contribution.

#### Periodic challenge

A weekly, lesson-block, or revision-period contest resets after a short period so that one early result does not create a permanent advantage.

#### Milestone challenge

Participants compete to satisfy a defined learning or preparation goal during the same fair availability window.

### 3.4 Trusted scoring

Scores may use meaningful events such as:

- verified practice results;
- improvement over a previous result;
- completion of defined challenge tasks;
- validated contributions;
- completion of a structured revision set;
- team progress from eligible member contributions.

Scores must not be based only on:

- logins;
- time online;
- page views;
- message count;
- repeated low-value actions;
- actions unrelated to learning or learner support.

### 3.5 Fair comparison groups

A global ranking across all learners should not be the default.

Where learners compete with others, the system should prefer groups that are reasonably comparable, such as:

- the same course instance;
- learners who opted in during the same registration window;
- learners at a similar course stage;
- study groups or teams of comparable size;
- a short challenge period with the same available tasks.

The scoring rule may use improvement, completion rate, or normalized results where raw totals would strongly favor learners with more time or earlier access.

### 3.6 Leaderboard and ranking display

The interface should show:

- challenge goal and rules;
- active period and time remaining;
- the learner's own score and eligibility;
- the comparison group;
- ranking or personal-best status;
- how ties are handled;
- whether results are provisional or final.

Possible privacy-preserving displays include:

- chosen display names or approved aliases;
- nearby ranks rather than the full leaderboard;
- top positions plus the learner's own position;
- team names instead of individual names;
- personal-best progress without public comparison.

The interface should not publicly label non-participants, inactive learners, or the lowest-ranked learners as failures.

### 3.7 Finalization and reward events

At the end of a challenge, the system should finalize valid scores before generating events such as:

- `COMPETITIVE_CHALLENGE_COMPLETED`;
- `COMPETITIVE_POSITION_CONFIRMED`;
- `PERSONAL_BEST_IMPROVED`;
- `COMPETITIVE_RESULT_REVOKED` after a correction.

Meaningful XP and Levels and Achievements and Badges decide the exact rewards. Participation alone does not need to produce XP unless the learner completed a meaningful learning requirement.

## 4. Motivation types supported

- **Competitors — strong:** comparison, status, personal bests, and limited rankings.
- **Achievers — medium:** clear goals, measurable results, and completion recognition.
- **Socializers — medium:** team contests and friendly group competition.
- **Explorers — low:** some competitions may allow different strategic paths, but discovery is not the main purpose.

## 5. Live-course behavior

- Registration and active periods may align with lesson blocks or exam preparation.
- Learners should receive the same meaningful opportunity window where possible.
- Cancelled or rescheduled lessons must update affected competition periods.
- Late enrollment must not place a learner into an already unfair ranking without a separate fair cohort or personal-best alternative.
- Attendance cannot be inferred from a lesson date passing.
- Competition should not require daily LMS visits unless the activity itself has a justified daily learning format.

## 6. Self-paced-course behavior

- Personal-best challenges are preferred where learners are at very different stages.
- Cohort competition may group learners who enter during a similar period or reach the same milestone.
- Scores should not reward finishing content earlier merely because a learner enrolled earlier.
- Taking a break outside an active, explicitly joined challenge does not create a penalty.
- Challenge windows and eligible content must be clear before the learner opts in.

## 7. Rules and edge cases

- Participation is opt-in and private by default outside the chosen comparison group.
- Not participating has no negative effect on normal course outcomes.
- A learner cannot enter the same individual competition multiple times using duplicate enrollments or accounts.
- The same source event cannot increase a score more than once unless distinct repeatable attempts are explicitly allowed.
- Rules must state whether the best, latest, first, or average attempt is used.
- Ties must use a declared rule, such as shared position or a meaningful secondary criterion.
- Earlier completion time should not be used as a tie-breaker unless all participants had the same fair start and the task is designed as a speed challenge.
- Staff corrections and removed source records must recalculate scores and ranks.
- Suspected collusion, plagiarism, account sharing, or manipulated activity may place results under review before finalization.
- Team rewards may require minimum verified individual contribution.
- Competition scores do not change required course progress unless the underlying activity independently satisfies a course requirement.
- A cancelled challenge does not award unearned placement rewards.
- A learner who withdraws should no longer appear in future public displays according to the announced withdrawal rule.
- Accessibility accommodations must not create automatic competitive disadvantage; personal-best or adjusted comparison formats may be used where appropriate.

## 8. Acceptance criteria

### AC1 — Explicit opt-in

Given an eligible learner has not joined a competitive challenge,
when the challenge is active,
then the learner is not included in its public participant list, scoring, or ranking.

### AC2 — No course penalty

Given a learner chooses not to participate,
when course completion and final-exam readiness are evaluated,
then non-participation has no negative effect.

### AC3 — Record a valid score

Given an opted-in learner performs a trusted scoring activity,
when the source event is processed,
then the learner's score is updated once according to the published rule.

### AC4 — Duplicate event

Given a source occurrence already contributed to a score,
when the same event is processed again,
then the score does not increase again.

### AC5 — Fair cohort

Given a challenge uses a cohort ranking,
when a learner joins,
then the learner is assigned only to a comparison group allowed by the published fairness rules.

### AC6 — Personal best

Given a personal-best challenge uses the learner's best verified result,
when the learner records a higher valid result,
then the personal best is updated
and one improvement event is generated.

### AC7 — Final ranking

Given the challenge period ends,
when valid scores and reviews are finalized,
then the ranking becomes final,
ties use the published rule,
and reward events are generated once.

### AC8 — Corrected score

Given a counted result is later invalidated,
when the correction is processed,
then the score and affected rankings are recalculated
and downstream reward systems receive a correction event.

### AC9 — Team contribution safeguard

Given a team earns a competitive placement
but one member did not satisfy the visible minimum individual contribution,
when personal rewards are evaluated,
then that member does not receive the configured individual placement reward solely because of membership.

### AC10 — Privacy after withdrawal

Given a learner withdraws according to the challenge rules,
when future leaderboard views are displayed,
then the learner's identity and future participation are handled according to the published privacy and withdrawal behavior.

## 9. Required LMS data

### Confirmed or provided by related feature requirements

- users, courses, course instances, and enrollment;
- Course Progress and Milestone events;
- XP and Achievement integrations;
- Study Group and Collaborative Challenge data when implemented;
- trusted assessment or contribution events where available.

### Missing or challenge-specific

- competitive challenge definitions and versions;
- explicit opt-in and withdrawal records;
- scoring attempts and source occurrences;
- cohort and comparison-group assignment;
- ranking snapshots and final results;
- review, dispute, and correction records;
- the final Challenge Catalogue and reward rules.

## 10. Model extensions

The supplied LMS models should not be modified.

### `CompetitiveChallengeDefinition`

Stores the purpose, format, eligibility, periods, scoring rules, comparison rules, tie handling, visibility, withdrawal behavior, reward event types, enabled status, and version.

### `CompetitiveChallengeInstance`

Stores the course-instance-specific challenge, active dates, status, comparison configuration, and finalization state.

### `CompetitiveParticipation`

Stores opt-in consent, withdrawal state, display preference, comparison group, eligibility, score, rank, and timestamps.

### `CompetitiveScoreEvent`

Stores the trusted source occurrence, attempt, score change, validation state, and processing key.

### `CompetitiveRankingSnapshot`

Stores provisional or final ranking results for auditing and display.

### `CompetitiveChallengeAuditEvent`

Stores rule changes, staff corrections, review decisions, cancellation, and finalization actions.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
