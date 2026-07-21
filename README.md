# LMS Gamification Requirements

This repository contains the current analysis and early business requirements for adding gamification to an existing Learning Management System (LMS).

## Assignment focus

The proposed gamification system must:

- increase learner retention, final-exam participation, and course completion;
- encourage meaningful communication between learners outside scheduled lessons;
- support both live and self-paced courses;
- avoid rewarding unnecessary website usage;
- account for different learner motivations;
- extend the existing LMS without modifying the supplied Mongoose models.

## Current problem

According to the project context discussed in the lecture, a course may attract roughly 650 enrollments, while only about 15–20% of the enrolled learners attend the final exam.

The main challenge is therefore not initial enrollment. It is keeping learners engaged and supported throughout the course until they reach the final exam and complete the course.

## Central design principle

> Reward meaningful learning progress, preparation, completion, and cooperation—not clicks, logins, or time spent on the website.

## Document maturity

All feature documents are rough functional outlines rather than final product specifications. Exact terminology, visual design, thresholds, reward amounts, model names, and implementation details may change after stakeholder, UX, and technical review.

The mechanics may also be presented through a stronger theme. For example, courses could appear as TTRPG-style campaign maps, study groups as adventuring parties, challenges as quests, optional challenges as side quests, and achievements as titles or artifacts. The functional rules should remain understandable independently of the final theme. See [`docs/document-status-and-theming.md`](docs/document-status-and-theming.md).

## Documentation

- [`docs/current-lms.md`](docs/current-lms.md) — map of the supplied LMS models and confirmed system capabilities.
- [`docs/purpose-and-goals.md`](docs/purpose-and-goals.md) — business problem, goals, non-goals, and success measures.
- [`docs/player-motivations.md`](docs/player-motivations.md) — Achievers, Socializers, Explorers, and Competitors.
- [`docs/feature-scope.md`](docs/feature-scope.md) — recommended feature scope and deliberately excluded features.
- [`docs/requirements-template.md`](docs/requirements-template.md) — structure to use when specifying each feature.
- [`docs/document-status-and-theming.md`](docs/document-status-and-theming.md) — maturity of the outlines and separation between functional rules and final theme.
- [`docs/course-progress.md`](docs/course-progress.md) — required, optional, and combined learner progress.
- [`docs/course-milestones.md`](docs/course-milestones.md) — configurable recognition of meaningful course checkpoints.
- [`docs/final-exam-readiness.md`](docs/final-exam-readiness.md) — exam readiness requirements, status, and missing actions.
- [`docs/achievements-and-badges.md`](docs/achievements-and-badges.md) — achievement awarding, badge display, scope, repeatability, privacy, and corrections.
- [`docs/meaningful-xp-and-levels.md`](docs/meaningful-xp-and-levels.md) — trusted XP transactions, levels, limits, duplicate prevention, and corrections.
- [`docs/badges-and-xp-sources.md`](docs/badges-and-xp-sources.md) — small initial list of possible badges and meaningful XP sources; exact reward details are deferred.
- [`docs/gamification-event-matrix.md`](docs/gamification-event-matrix.md) — proposed event ownership, availability, consumers, and correction flow.
- [`docs/mvp-prioritization.md`](docs/mvp-prioritization.md) — essential MVP, recommended follow-up, later expansion, and optional competition.
- [`docs/consistency-review.md`](docs/consistency-review.md) — terminology, feature boundaries, corrections, and remaining implementation decisions.
- [`docs/course-q-and-a-and-peer-help.md`](docs/course-q-and-a-and-peer-help.md) — course-instance questions, answers, comments, accepted solutions, closure, and moderation.
- [`docs/peer-contribution-recognition.md`](docs/peer-contribution-recognition.md) — validation and recognition of useful peer support without rewarding message volume.
- [`docs/study-groups.md`](docs/study-groups.md) — small course-instance learning groups, membership, access, and safeguards.
- [`docs/collaborative-challenges.md`](docs/collaborative-challenges.md) — shared learning goals, team progress, individual contribution, and fair rewards.
- [`docs/optional-exploration-challenges.md`](docs/optional-exploration-challenges.md) — voluntary discovery paths, side activities, optional progress, and safeguards.
- [`docs/opt-in-competitive-challenges.md`](docs/opt-in-competitive-challenges.md) — voluntary personal-best, cohort, and team competitions with fairness and privacy rules.

## Current status

The existing LMS has been mapped and the purpose, motivation framework, and initial feature scope have been defined. Rough feature outlines are now available for Course Progress, Course Milestones, Final Exam Readiness, Achievements and Badges, Meaningful XP and Levels, Course Q&A and Peer Help, Peer Contribution Recognition, Study Groups, Collaborative Challenges, Optional Exploration Challenges, and Opt-in Competitive Challenges. A proposed event matrix, MVP prioritization, and final consistency review are also included.

## Important limitation

The existing website interface, application logic, and several referenced models were not supplied. Requirements concerning screens, attendance, discussions, and assessment results must therefore be documented as assumptions or as new tracking capabilities.
