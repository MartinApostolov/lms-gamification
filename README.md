# LMS Gamification Requirements

This repository contains the current analysis and revised business requirements for adding gamification to an existing Learning Management System (LMS).

## Assignment focus

The proposed gamification system must:

- increase learner retention, final-exam participation, and course completion;
- encourage meaningful cooperation between learners outside scheduled lessons;
- support both live and self-paced courses;
- avoid rewarding unnecessary website usage;
- account for different learner motivations;
- extend the existing LMS without modifying the supplied Mongoose models.

## Current problem

According to the project context discussed in the lecture, a course may attract roughly 650 enrollments, while only about 15–20% of the enrolled learners attend the final exam.

The main challenge is therefore not initial enrollment. It is keeping learners engaged and supported throughout the course until they reach the final exam and complete the course, then helping them retain important knowledge afterward.

## Central design principle

> Reward meaningful learning progress, preparation, completion, cooperation, and retained knowledge—not clicks, logins, reactions, message volume, or time spent on the website.

## Current implementation focus

The scope was revised after stakeholder feedback.

The main implementation direction is:

- course-instance Study Groups;
- Collaborative Challenges assigned to groups or teams;
- visible shared progress;
- verified individual contribution;
- separate group completion and personal reward eligibility;
- limited meaningful XP and achievements connected to trusted challenge events.

The recommended extension is:

- Post-course Knowledge Refreshers;
- short optional revision activities;
- topic-level feedback;
- links back to relevant completed material;
- future Skill Profile integration.

General Course Q&A and reaction-based Peer Contribution Recognition were removed from active scope. The reasons are documented in [`docs/stakeholder-feedback-and-scope-revision.md`](docs/01-project-context/stakeholder-feedback-and-scope-revision.md).

## Document maturity

All feature documents are rough functional outlines rather than final product specifications. Exact terminology, visual design, thresholds, reward amounts, model names, and implementation details may change after stakeholder, UX, and technical review.

A later interface may use a stronger visual theme, but the business requirements use plain functional terminology. See [`docs/document-status-and-theming.md`](docs/02-planning-and-standards/document-status-and-theming.md).

## Documentation

See the [organized documentation index](docs/README.md) for the folder-by-folder structure.

### Scope and analysis

- [`docs/current-lms.md`](docs/01-project-context/current-lms.md) — map of the supplied LMS models and confirmed system capabilities.
- [`docs/purpose-and-goals.md`](docs/01-project-context/purpose-and-goals.md) — business problem, goals, non-goals, and success measures.
- [`docs/player-motivations.md`](docs/01-project-context/player-motivations.md) — Achievers, Socializers, Explorers, and Competitors.
- [`docs/stakeholder-feedback-and-scope-revision.md`](docs/01-project-context/stakeholder-feedback-and-scope-revision.md) — lecturer feedback, removed features, and revised focus.
- [`docs/feature-scope.md`](docs/02-planning-and-standards/feature-scope.md) — active, supporting, later, future, and excluded features.
- [`docs/mvp-prioritization.md`](docs/02-planning-and-standards/mvp-prioritization.md) — implementation tiers and the recommended demonstration flow.
- [`docs/requirements-template.md`](docs/02-planning-and-standards/requirements-template.md) — structure to use when specifying a feature.
- [`docs/document-status-and-theming.md`](docs/02-planning-and-standards/document-status-and-theming.md) — maturity of the outlines and separation between functional rules and presentation.
- [`docs/consistency-review.md`](docs/02-planning-and-standards/consistency-review.md) — terminology, feature boundaries, corrections, and remaining decisions.

### Primary implementation features

- [`docs/study-groups.md`](docs/03-primary-features/study-groups.md) — small course-instance learning groups, membership, access, roles, and safeguards.
- [`docs/collaborative-challenges.md`](docs/03-primary-features/collaborative-challenges.md) — shared learning goals, group progress, individual contribution, completion, and fair rewards.
- [`docs/post-course-knowledge-refreshers.md`](docs/03-primary-features/post-course-knowledge-refreshers.md) — optional post-course revision, timing, attempts, feedback, review links, and corrections.

### Supporting mechanics

- [`docs/course-progress.md`](docs/04-supporting-mechanics/course-progress.md) — required, optional, and combined learner progress.
- [`docs/course-milestones.md`](docs/04-supporting-mechanics/course-milestones.md) — configurable recognition of meaningful course checkpoints.
- [`docs/final-exam-readiness.md`](docs/04-supporting-mechanics/final-exam-readiness.md) — exam readiness requirements, status, and missing actions.
- [`docs/meaningful-xp-and-levels.md`](docs/04-supporting-mechanics/meaningful-xp-and-levels.md) — trusted XP transactions, levels, limits, duplicate prevention, and corrections.
- [`docs/achievements-and-badges.md`](docs/04-supporting-mechanics/achievements-and-badges.md) — achievement awarding, badge display, scope, repeatability, privacy, and corrections.
- [`docs/badges-and-xp-sources.md`](docs/04-supporting-mechanics/badges-and-xp-sources.md) — small initial list of possible badges and meaningful XP sources.
- [`docs/gamification-event-matrix.md`](docs/06-integrations/gamification-event-matrix.md) — proposed event ownership, availability, consumers, and correction flow.

### Later variants and future integration

- [`docs/optional-exploration-challenges.md`](docs/05-later-features/optional-exploration-challenges.md) — voluntary discovery paths, side activities, optional progress, and safeguards.
- [`docs/opt-in-competitive-challenges.md`](docs/05-later-features/opt-in-competitive-challenges.md) — voluntary personal-best, cohort, and team competitions with fairness and privacy rules.
- [`docs/future-skill-profile-integration.md`](docs/06-integrations/future-skill-profile-integration.md) — future skill evidence, course recommendations, and adaptive self-paced path boundaries.

### Source note

- [`docs/source-note.md`](docs/01-project-context/source-note.md) — note about the supplied LMS model evidence.

## Current status

The existing LMS has been mapped, the purpose and motivation framework have been defined, and the scope has been narrowed after stakeholder feedback.

The primary implementation requirements now cover Study Groups and Collaborative Challenges. Post-course Knowledge Refreshers are documented as the recommended extension. Course Progress, Course Milestones, Final Exam Readiness, Meaningful XP and Levels, and Achievements and Badges remain supporting requirements.

A proposed event matrix, MVP prioritization, future Skill Profile integration boundary, and final consistency review are included.

## Important limitation

The existing website interface, application logic, and several referenced models were not supplied. Requirements concerning screens, attendance, group communication, assessment results, refreshers, and skill data must therefore be documented as assumptions or as new tracking capabilities.
