# Meaningful XP and Levels

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Meaningful XP and Levels provides immediate, cumulative recognition for verified learning progress, preparation, completion, exploration, and helpful participation.

**XP** is a non-spendable measure of recognized activity. **Levels** are account-wide stages reached when a learner accumulates enough valid XP.

Learners should be able to:

- view their current XP and level;
- see how much XP remains before the next level;
- view a history explaining where XP came from;
- distinguish learning, optional, examination, and contribution XP where useful.

Authorized staff should be able to configure XP rules, review transactions, and correct invalid awards.

XP must not replace course progress. A learner may have a high level while still being incomplete in a particular course, and XP must never determine course completion or final-exam eligibility unless an explicit requirement separately refers to the underlying learning activity.

A small set of possible earning sources is listed in **Initial Badges and XP Sources**. Exact XP amounts, limits, and level thresholds remain deferred until implementation.

## 2. Why

Course completion and major badges may be too distant to provide frequent feedback. XP gives learners small but meaningful recognition between larger milestones, while levels provide a longer-term sense of development across courses.

The feature supports:

- regular acknowledgement of real progress;
- visible long-term development across the LMS;
- recognition of optional learning without making it mandatory;
- recognition of validated peer support;
- later achievement and challenge integrations.

XP must reward educational value, not website usage. Logins, page views, time online, raw message count, repeated actions, and unvalidated reactions must not award XP.

## 3. How

### 3.1 XP earning rules

Every XP rule should define:

- the trusted event or validated action that triggers it;
- the XP amount;
- its scope, such as global, course, course instance, or challenge;
- whether it is one-time or repeatable;
- any daily, weekly, course, or lifetime limit;
- its rule version and enabled status;
- whether a correction may reverse the award.

Possible source categories include:

- required or optional course activities;
- course milestones;
- final-exam readiness, attendance, or completion;
- course or program completion;
- validated peer contributions;
- study-group participation tied to a real activity;
- collaborative or optional challenges;
- authorized manual awards.

This list identifies possible sources only. Exact triggers and values belong in the later rules catalogue.

### 3.2 XP transaction ledger

Every XP change should be stored as a transaction rather than directly overwriting a total.

A transaction should record:

- learner;
- positive or negative XP amount;
- rule and rule version;
- source event or validated contribution;
- related course, course instance, group, or challenge when applicable;
- awarded or corrected time;
- status and reason;
- awarding or correcting staff member for manual actions.

The learner’s current XP is the sum of active transactions. The transaction ledger supports explanation, duplicate prevention, auditing, and correction.

### 3.3 Duplicate prevention and limits

One source occurrence must create no more than one XP transaction for the same rule.

Repeatable rules must state what counts as a new valid occurrence. For example, separate accepted solutions may be distinct occurrences, while repeated editing or reopening of one answer is not.

Configurable caps or diminishing returns may be used for repeatable social actions so that XP encourages useful participation without encouraging farming.

### 3.4 Levels

Levels should use configurable XP thresholds. Thresholds must increase and should be understandable to learners.

Levels are account-wide by default because they represent development across the LMS. Course-specific XP totals may be displayed as supporting statistics but do not create separate learner levels in the first version.

Reaching a level may generate a trusted `LEVEL_REACHED` event for Achievements and Badges. A level does not automatically grant course credit, exam eligibility, authority, or material benefits.

### 3.5 Corrections and rule changes

If XP was awarded from incorrect data, fraud, a revoked contribution, or an incorrect manual decision, an authorized correction should create a reversing transaction. The original transaction remains in the audit history.

Current XP and level are recalculated after a reversal. A learner’s level may decrease when invalid XP is removed, but a later rule-value change should not retroactively alter valid historical transactions unless an administrator explicitly runs a documented migration.

### 3.6 Learner display

A compact display may show:

```text
Level 4
1,260 XP
240 XP to Level 5
```

The detailed history should use understandable reasons, for example:

```text
+40 XP — Reached the Halfway course milestone
+20 XP — Answer accepted as the solution
+30 XP — Completed an optional practice challenge
```

The interface should not imply that XP is the same as academic grade, course percentage, or exam score.

## 4. Motivation types supported

- **Achievers — strong:** cumulative progress, levels, and visible next thresholds.
- **Socializers — medium:** validated helpful participation can earn recognition.
- **Explorers — medium:** optional activities may award XP without affecting required progress.
- **Competitors — medium:** XP may support opt-in comparisons, but public ranking is outside this feature.

## 5. Live-course behavior

- XP uses confirmed activity and attendance, not a scheduled date simply passing.
- Cancelled or rescheduled lessons must use corrected source events.
- Late-enrolling learners may earn XP for requirements they actually complete.
- Learners are not penalized for days without LMS activity.
- Repeated visits between scheduled lessons do not award XP.

## 6. Self-paced-course behavior

- Learners may earn several valid XP transactions in one session.
- Taking a break does not reduce XP.
- Reopening completed content does not award XP again.
- Time-based earning rules should be used only for meaningful, explicitly time-limited activities.

## 7. Rules and edge cases

- XP is not a spendable currency in the first version.
- XP does not affect required or optional course-progress percentages.
- XP does not by itself satisfy final-exam readiness.
- No XP is awarded for login streaks, page views, time online, raw posts, raw comments, or raw reactions.
- Manual XP requires an authorized role and a recorded reason.
- A disabled rule creates no new transactions; valid existing transactions remain.
- Processing the same event more than once must be idempotent.
- Public XP or level comparison requires a separate opt-in competitive feature.
- Deleting or unaccepting a rewarded contribution may reverse its XP according to the applicable rule.

## 8. Acceptance criteria

### AC1 — Valid XP award

Given an enabled XP rule has a trusted source event,
when the learner satisfies the rule,
then one XP transaction is created with the correct amount, source, scope, rule version, and time.

### AC2 — Duplicate source event

Given an XP transaction already exists for a source occurrence and rule,
when the same source event is processed again,
then no duplicate XP is added.

### AC3 — Level calculation

Given a learner’s active XP reaches a configured level threshold,
when XP is recalculated,
then the learner’s current level is updated
and the level is displayed with the correct next threshold.

### AC4 — No XP for raw activity

Given a learner logs in, opens pages, remains online, or posts an unvalidated message,
when those actions are processed,
then no XP transaction is created.

### AC5 — Accepted solution source

Given another learner’s answer is validly marked as the accepted solution
and the applicable contribution XP rule is enabled,
when the validation event is processed,
then the answerer receives the configured XP once.

### AC6 — Reversal

Given XP was awarded from an invalid or revoked source,
when an authorized correction is processed,
then a reversing transaction is created
and current XP and level are recalculated.

### AC7 — Course independence

Given a learner has accumulated global XP,
when the learner begins a new course,
then their global level remains available
but the new course progress begins according to that course’s own requirements.

### AC8 — Rule change

Given a valid XP transaction was created under an earlier rule version,
when the XP value for future awards changes,
then the historical transaction keeps its original value unless an explicit audited migration is performed.

## 9. Required LMS data

### Confirmed or provided by completed feature requirements

- users, courses, course instances, and programs;
- lesson and course completion events;
- Course Progress, Course Milestone, Final Exam Readiness, and Achievement events where their source data exists.

### Missing or dependent on later features

- validated question answers and accepted solutions;
- study-group participation;
- collaborative and optional challenge results;
- reliable final-exam attendance and some assessment outcomes;
- final XP amounts and level thresholds.

XP rules depending on missing events must remain disabled until the source is reliable.

## 10. Model extensions

The supplied LMS models should not be modified.

### `XPRule`

Stores the source event, XP amount, scope, repeatability, limits, enabled status, and rule version.

### `XPTransaction`

Stores the learner, signed XP amount, rule, source occurrence, scope references, status, reason, timestamps, and manual actor where applicable.

### `LearnerLevel`

Stores or caches the learner’s current XP, current level, next threshold, and last calculation time. The transaction ledger remains the source of truth.

## 11. Success measure

Measure whether XP users show stronger movement through meaningful course stages without an increase in low-value activity.

Useful indicators include:

- percentage of active learners earning XP from meaningful sources;
- movement from course start to halfway, exam readiness, exam attendance, and completion;
- proportion of XP coming from learning, optional, examination, and validated contribution sources;
- duplicate, reversed, or abuse-related XP transactions;
- relationship between level progression and course completion.

Raw website time and message count are not success measures.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
