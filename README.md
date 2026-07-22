# LMS Gamification Requirements

This repository contains the current analysis, business requirements, and implementation-planning material for adding gamification to an existing Learning Management System (LMS).

## Assignment focus

The proposed gamification system must:

- increase learner retention, final-exam participation, and course completion;
- encourage meaningful cooperation between learners outside scheduled lessons;
- support both live and self-paced course instances;
- avoid rewarding unnecessary website usage;
- account for different learner motivations;
- extend the existing LMS through separate models and integrations rather than modifying the supplied core models.

## Current problem

According to the project context discussed in the lecture, a course may attract roughly 650 enrollments, while only about 15–20% of enrolled learners attend the final exam.

The main challenge is therefore not initial enrollment. It is keeping learners engaged and supported throughout the course until they reach the final exam and complete the course, then helping them retain important knowledge afterward.

## Central design principle

> Reward meaningful learning progress, preparation, completion, cooperation, and retained knowledge—not clicks, logins, reactions, message volume, time online, or random activity indicators.

## Evidence reviewed

The documentation was first created from a limited set of exported Mongoose models. It has now been updated after reviewing the full supplied LMS mock-up, including:

- backend models, services, controllers, routes, and authorization middleware;
- frontend learner, teacher, content-manager, and administrator screens;
- course, course-instance, lesson-completion, assessment, exam, certificate, program, and survey flows;
- seed data and the current placeholder Activity Tracker.

The source-grounded review is recorded in:

- [Current LMS Map](docs/01-project-context/current-lms.md);
- [Detailed Current LMS Maps](docs/01-project-context/current-lms/README.md);
- [Mock-up Requirements Impact Review](docs/02-planning-and-standards/mockup-requirements-impact-review.md).

## Current implementation direction

The main product identity remains:

> Study Groups with Collaborative Challenges, supported by meaningful progress and rewards, followed by optional Post-course Knowledge Refreshers.

The recommended first demonstration path is:

1. secure and de-duplicate trusted source events;
2. show Course Progress for one tracked Course Instance;
3. create or assign a Study Group;
4. assign one Collaborative Challenge;
5. record verified individual contributions and shared progress;
6. distinguish group completion from personal reward eligibility;
7. award limited XP and one achievement exactly once;
8. display the result in Course Details and Profile.

The next implementation stage can add Final Exam Readiness using the mock-up's real exam enrollment, scheduling, instructions, submissions, scores, and pass/fail data. Post-course Knowledge Refreshers remain the recommended later extension.

General Course Q&A and reaction-based Peer Contribution Recognition were removed from active scope. The reasons are documented in [Stakeholder Feedback and Scope Revision](docs/01-project-context/stakeholder-feedback-and-scope-revision.md).

## Document maturity

All feature documents are rough functional outlines rather than final product or technical specifications. Exact terminology, visual design, thresholds, XP amounts, badge artwork, payloads, schemas, and implementation details may change during coding and stakeholder review.

A later interface may use a stronger visual theme, but the requirements use plain functional terminology. See [Document Status and Theming](docs/02-planning-and-standards/document-status-and-theming.md).

## Documentation

See the [organized documentation index](docs/README.md) for the complete folder structure.

### Project context and source analysis

- [Current LMS Map](docs/01-project-context/current-lms.md)
- [Detailed Current LMS Maps](docs/01-project-context/current-lms/README.md)
- [Purpose and Goals](docs/01-project-context/purpose-and-goals.md)
- [Player Motivations](docs/01-project-context/player-motivations.md)
- [Stakeholder Feedback and Scope Revision](docs/01-project-context/stakeholder-feedback-and-scope-revision.md)
- [Source Note](docs/01-project-context/source-note.md)

### Planning and standards

- [Feature Scope](docs/02-planning-and-standards/feature-scope.md)
- [MVP Prioritization](docs/02-planning-and-standards/mvp-prioritization.md)
- [Mock-up Requirements Impact Review](docs/02-planning-and-standards/mockup-requirements-impact-review.md)
- [Requirements Template](docs/02-planning-and-standards/requirements-template.md)
- [Document Status and Theming](docs/02-planning-and-standards/document-status-and-theming.md)
- [Consistency Review](docs/02-planning-and-standards/consistency-review.md)

### Primary implementation features

- [Study Groups](docs/03-primary-features/study-groups.md)
- [Collaborative Challenges](docs/03-primary-features/collaborative-challenges.md)
- [Post-course Knowledge Refreshers](docs/03-primary-features/post-course-knowledge-refreshers.md)

### Supporting mechanics

- [Course Progress](docs/04-supporting-mechanics/course-progress.md)
- [Course Milestones](docs/04-supporting-mechanics/course-milestones.md)
- [Final Exam Readiness](docs/04-supporting-mechanics/final-exam-readiness.md)
- [Meaningful XP and Levels](docs/04-supporting-mechanics/meaningful-xp-and-levels.md)
- [Achievements and Badges](docs/04-supporting-mechanics/achievements-and-badges.md)
- [Initial Badges and XP Sources](docs/04-supporting-mechanics/badges-and-xp-sources.md)

### Later variants and integrations

- [Optional Exploration Challenges](docs/05-later-features/optional-exploration-challenges.md)
- [Opt-in Competitive Challenges](docs/05-later-features/opt-in-competitive-challenges.md)
- [Gamification Event Matrix](docs/06-integrations/gamification-event-matrix.md)
- [Future Skill Profile Integration](docs/06-integrations/future-skill-profile-integration.md)

## Current status

The requirements phase is substantially complete and grounded in the supplied full LMS mock-up. The Current LMS Map, entity relationships, workflows, feature boundaries, event ownership, MVP sequence, and main integration risks are documented.

Application code has not yet been added to this requirements repository. Implementation is planned for a later stage against the supplied LMS mock-up.

## Main implementation decisions still open

Before or during coding, the team must decide:

- which tracked lessons are required, optional, or excluded from Course Progress;
- whether Course Progress is enabled only for `isTracked` Course Instances;
- how repeated Course Instances of the same Course are represented in progress and rewards;
- which roles may create groups, assign challenges, validate contributions, and reverse rewards;
- whether group communication is built into the LMS or uses an approved external integration;
- which exam conditions are readiness requirements rather than informational preparation steps;
- how corrected assessment results, revoked completion, and reward reversals are represented;
- whether the placeholder Activity Tracker is removed, hidden, or rebuilt from meaningful events.

The existing Activity Tracker must not be treated as trusted gamification data because its current values are random and client-only.
