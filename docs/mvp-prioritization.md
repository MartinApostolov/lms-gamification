# MVP Prioritization

> **Document status:** This is a rough release-planning outline. Priorities may change after stakeholder review, technical discovery, and confirmation of available LMS data.

## 1. Prioritization goal

The first implementation should address the main business problem: learners enroll but many do not remain active through the final exam and course completion.

Priority is therefore based on:

1. direct connection to course retention and final-exam participation;
2. availability and reliability of source data;
3. ability to prevent duplicate or farmed rewards;
4. implementation dependency on earlier features;
5. value for more than one learner motivation type.

## 2. Tier 0 — Required technical foundation

This is not a separate learner-facing feature, but it is required before meaningful rewards are reliable.

- trusted event or change-detection layer;
- unique source-occurrence identifiers and idempotent processing;
- audit history for corrections and manual validation;
- course-instance-based learner scope;
- configuration and rule versioning;
- permission checks for staff corrections.

Without this foundation, XP, achievements, milestones, and challenge results may be duplicated or become impossible to correct safely.

## 3. Tier 1 — Essential MVP

### Course Progress

Initial scope:

- required lesson progress from 0–100;
- optional progress only where optional activities are reliably configured;
- combined points out of 200 when optional progress exists;
- next recommended required activity;
- separate progress for each course instance.

Reason: this directly makes the route to completion visible and uses the strongest confirmed data source: lesson completion.

### Course Milestones

Initial scope:

- Course Started;
- 25%, 50%, 75%, and Required Work Complete;
- one milestone record per learner, course instance, and definition;
- no ordinary milestone notifications.

Reason: milestones turn progress into smaller meaningful goals and provide trusted reward triggers.

### Final Exam Readiness

Initial scope:

- configurable checklist and status;
- readiness based on data that is actually available;
- manual staff confirmation only where automatic tracking is unavailable and auditing is possible;
- exam-related events exposed to a separate notification mechanism.

Reason: this is directly connected to the primary business goal. The scope may initially be limited because exam attendance and assessment data are not confirmed.

### Meaningful XP and Levels

Initial scope:

- XP transaction ledger;
- a small number of one-time or low-frequency rules based on trusted progress, milestone, exam, and course-completion events;
- account-wide level calculation;
- no XP for logins, time online, raw posts, or repeated completion.

Reason: gives frequent recognition while relying on the core trusted events.

### Achievements and Badges

Initial scope:

- a small set of working badges from the Initial Badges and XP Sources document;
- automatic awards from trusted events;
- duplicate prevention, privacy, and correction history;
- no complete badge catalogue or final artwork required.

Reason: provides memorable recognition without requiring the full social and challenge system.

## 4. Tier 2 — Recommended after the core MVP

### Course Q&A and Peer Help

- course-instance questions, answers, and comments;
- one accepted solution;
- close, reopen, moderate, and audit;
- no reward for posting alone.

### Peer Contribution Recognition

- recognition for accepted solutions and other authorized useful contributions;
- contribution limits and anti-farming checks;
- trusted events for XP and achievements.

Reason: these two features address the secondary goal of meaningful communication and should be delivered together. The Q&A feature creates the interaction; Peer Contribution Recognition validates what deserves a reward.

## 5. Tier 3 — Later expansion

### Study Groups

Adds small course-instance communities, membership, roles, privacy, and staff oversight.

### Collaborative Challenges

Adds shared goals and verified individual contributions. It depends on reliable groups or team membership and trusted challenge events.

### Optional Exploration Challenges

Adds voluntary side activities and optional progress. It should follow the core progress and reward foundations so optional work remains clearly separate from required completion.

Reason: these features provide strong additional value but require more new models, moderation, configuration, and content design than the core MVP.

## 6. Tier 4 — Optional later feature

### Opt-in Competitive Challenges

Adds personal-best, cohort, team, or ranking-based challenges with opt-in consent, fair comparison groups, privacy, tie rules, and score finalization.

Reason: competition supports only part of the learner population and carries higher fairness, privacy, and discouragement risks. It should be introduced only after the non-competitive system is stable.

## 7. Theming and presentation

A TTRPG-inspired presentation can be explored after the core functional rules are validated. It does not need to wait until every later feature exists.

A first themed release could represent:

- the course as an adventure map;
- required progress as the main journey;
- optional progress as exploration paths;
- milestones as landmarks;
- study groups as adventuring parties;
- challenges as quests;
- achievements as titles or artifacts.

Plain-language labels should remain available so the interface is understandable to learners who are unfamiliar with the theme.

## 8. Suggested implementation sequence

1. Event, audit, and configuration foundation.
2. Course Progress.
3. Course Milestones.
4. Limited Final Exam Readiness.
5. Basic XP, Levels, Achievements, and Badges.
6. Course Q&A and Peer Help.
7. Peer Contribution Recognition.
8. Study Groups.
9. Collaborative Challenges.
10. Optional Exploration Challenges.
11. Opt-in Competitive Challenges.

The exact sequence may change if exam or communication capabilities already exist outside the supplied models.
