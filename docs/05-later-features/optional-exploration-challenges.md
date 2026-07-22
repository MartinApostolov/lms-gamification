# Optional Exploration Challenges

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](../02-planning-and-standards/document-status-and-theming.md).

## 1. What

Optional Exploration Challenges give learners voluntary, course-related activities beyond the required learning path.

They may provide additional practice, connected resources, alternative approaches, deeper investigation, or discoverable activities. In a themed interface, they could be presented as **side quests**, optional locations, or branches on a course map.

This document defines the framework for optional exploration challenges. It does not define the final list of activities, XP values, achievements, or themed names. Those should be maintained later in a **Challenge Catalogue**.

## 2. Why

Some learners are motivated by discovery, choice, and the opportunity to go beyond the minimum requirements.

Optional exploration can:

- give Explorer-type learners additional motivation;
- provide more practice without delaying other learners;
- recognize curiosity and independent learning;
- offer alternative ways to apply course knowledge;
- help learners discover related topics and resources;
- create additional goals after required work is complete.

The feature must not turn optional browsing into a hidden course requirement or encourage meaningless website activity.

## 3. How

### 3.1 Challenge definition

An exploration challenge should define:

- title, description, and learning purpose;
- related course, course instance, lesson, milestone, or topic;
- eligibility and optional prerequisites;
- whether it is visible immediately or meaningfully discoverable;
- trusted completion requirements;
- optional-progress contribution;
- event types available to XP and Achievements;
- availability dates or course-stage rules;
- repeatability and maximum completions;
- enabled status and rule version.

### 3.2 Possible challenge types

Possible formats include:

- additional practice tasks;
- applying a lesson to a new example;
- exploring an approved external or internal resource;
- finding connections between course topics;
- solving an alternative version of a problem;
- producing an optional explanation, example, or learning resource;
- completing a branching learning path;
- discovering a challenge through a meaningful course clue;
- optional preparation beyond the normal exam requirements.

Opening a resource or finding a hidden button is not enough by itself. Completion should require a meaningful action where possible.

### 3.3 Required, optional, and combined progress

Exploration challenges may contribute to the learner's **optional progress from 0–100**.

They do not increase required progress and cannot be required for:

- completing the normal course;
- reaching 100% required progress;
- becoming eligible for the final exam;
- receiving the standard course-completion record.

Course Progress may display:

- Required progress: 100 / 100
- Optional progress: 45 / 100
- Combined progress: 145 / 200

The optional-progress value assigned to each challenge should be configured in the Challenge Catalogue or course rules.

### 3.4 Visible and discoverable challenges

A challenge may be:

1. **Visible** — shown directly in an optional activities list; or
2. **Discoverable** — revealed after a meaningful learning action, clue, topic connection, or prerequisite.

Discoverable challenges must not require random page visits, repeated clicking, inspection of unrelated pages, or excessive time on the LMS.

The system may show that optional discoveries exist without revealing every detail. Learners who do not find them must not lose required progress or exam eligibility.

### 3.5 Completion and reward events

When a learner satisfies the trusted completion condition, the feature should generate events such as:

- `EXPLORATION_CHALLENGE_COMPLETED`;
- `OPTIONAL_PROGRESS_UPDATED`;
- `EXPLORATION_CHALLENGE_COMPLETION_REVOKED` when the source completion is invalidated.

Meaningful XP and Levels and Achievements and Badges decide whether and how the event is rewarded. This feature does not set exact XP amounts or badge designs.

### 3.6 Learner choice

Learners should be able to choose which optional paths interest them. A course may offer more optional challenge value than is needed to reach 100 optional progress so that learners are not forced to complete every available activity.

Where several paths award equivalent optional progress, the interface should explain that they are alternatives.

## 4. Motivation types supported

- **Explorers — strong:** discovery, optional paths, additional knowledge, and choice.
- **Achievers — medium:** visible optional completion and extra goals.
- **Socializers — low to medium:** some exploration tasks may involve sharing an approved resource or explanation.
- **Competitors — low:** exploration is primarily personal and should not require ranking.

## 5. Live-course behavior

- Challenges may unlock after a scheduled lesson, course milestone, or lecturer announcement.
- A learner who misses a live lesson should not permanently lose optional progress when a reasonable alternative is available.
- Rescheduled or cancelled lessons should update related challenge availability.
- The feature should not require daily LMS use unless the optional learning activity itself meaningfully depends on a daily practice schedule.
- Late-enrolling learners should see currently available challenges and any clearly marked expired optional activities.

## 6. Self-paced-course behavior

- Challenges may unlock according to the learner's own progress rather than calendar dates.
- Learners may complete several optional challenges in one session.
- Taking a break does not reduce optional progress.
- Reopening completed materials does not produce additional progress or rewards.
- Availability windows should be used only where they serve a genuine learning purpose.

## 7. Rules and edge cases

- Exploration challenges are optional and cannot silently become completion requirements.
- Opening, viewing, or clicking an item does not prove completion unless viewing is itself the meaningful requirement and can be verified appropriately.
- The same source occurrence cannot complete the same challenge repeatedly unless repeatability is explicitly configured.
- Optional progress remains between 0 and 100 even when more optional challenge value is available.
- Combined progress remains between 0 and 200.
- Completing optional work after required course completion remains valid when the course instance still permits access.
- A removed or corrected completion recalculates optional progress and creates downstream correction events.
- Expired challenges should remain visible in history when already completed.
- External resources must be approved, accessible, and connected to a stated learning purpose.
- Discoverable challenges must not depend on inaccessible visual clues alone.
- A course manager may disable a challenge for future learners without silently deleting existing completion history.

## 8. Acceptance criteria

### AC1 — View optional challenges

Given a learner is enrolled in an eligible course instance,
when optional challenges are available,
then the learner can distinguish them from required course activities
and can see that they do not block normal completion.

### AC2 — Complete a verified challenge

Given a learner satisfies the trusted requirements of an enabled exploration challenge,
when completion is processed,
then the challenge is recorded as completed once
and the configured optional progress is added once.

### AC3 — Required progress is unchanged

Given a learner completes an optional exploration challenge,
when Course Progress is recalculated,
then optional and combined progress may increase
but required progress does not increase.

### AC4 — Duplicate completion

Given a non-repeatable challenge is already complete,
when the same source event is processed again,
then optional progress and rewards do not increase again.

### AC5 — Discoverable challenge

Given a challenge is configured as discoverable,
when the learner satisfies its meaningful reveal condition,
then the challenge becomes available without requiring unrelated browsing or random clicking.

### AC6 — Course completion safeguard

Given a learner has not completed any optional challenges
but has satisfied all required course-completion rules,
when completion is evaluated,
then the learner can still complete the course and meet standard exam eligibility rules.

### AC7 — Choice between paths

Given multiple alternative challenges can satisfy the same optional-progress allocation,
when the learner completes one valid path,
then the configured progress is awarded
without requiring completion of every alternative.

### AC8 — Corrected completion

Given a recorded challenge completion is later invalidated,
when the correction is processed,
then optional and combined progress are recalculated
and affected reward systems receive a correction event.

## 9. Required LMS data

### Confirmed or provided by related feature requirements

- users, courses, course instances, and enrollment;
- required and optional Course Progress;
- Course Milestone events;
- XP and Achievement integrations.

### Missing or challenge-specific

- exploration challenge definitions and versions;
- reveal and eligibility conditions;
- trusted completion records for new activity types;
- approved resource metadata;
- alternative-path relationships;
- the final Challenge Catalogue and reward values.

## 10. Model extensions

The supplied LMS models should not be modified.

### `ExplorationChallengeDefinition`

Stores the learning purpose, scope, visibility mode, eligibility, prerequisites, completion rules, optional-progress value, repeatability, availability, event types, enabled status, and version.

### `ExplorationChallengeInstance`

Stores a course-instance-specific use of a definition and any overridden availability or configuration.

### `UserExplorationChallenge`

Stores the learner, challenge instance, reveal state, progress, completion status, trusted source occurrences, and timestamps.

### `ExplorationChallengeAuditEvent`

Stores configuration changes, manual corrections, invalidations, and staff actions.

## 11. Success measure

Useful indicators include:

- percentage of eligible learners who discover and start optional challenges;
- completion rate by challenge type and difficulty;
- use of alternative paths and connected resources;
- movement from optional activity to later required milestones or course completion;
- percentage of optional progress generated without affecting required completion;
- correction, duplicate, or abuse-related events;
- learner feedback on choice, usefulness, and clarity.

Success is meaningful optional learning and discovery, not the amount of time spent browsing for hidden content.

See [Gamification Event Matrix](../06-integrations/gamification-event-matrix.md) for proposed event ownership and integrations.
