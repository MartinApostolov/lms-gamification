# MVP Prioritization

> **Document status:** This is a rough release-planning outline revised after stakeholder review and grounded in the supplied full LMS mock-up. Priorities may still change during implementation because of available time, integration constraints, and stakeholder decisions.

## 1. Prioritization goal

The implementation should demonstrate one coherent system that can later be reused or integrated into a larger LMS.

Priority is based on:

1. direct connection to retention, preparation, and completion;
2. clarity of the learner flow during review;
3. reuse across live and self-paced courses;
4. reliable source data and duplicate prevention;
5. ability to integrate with other students' features;
6. realistic implementation scope.

The active focus is Study Groups and Collaborative Challenges. Post-course Knowledge Refreshers are the recommended extension.

See [Stakeholder Feedback and Scope Revision](../01-project-context/stakeholder-feedback-and-scope-revision.md) and [Mock-up Requirements Impact Review](mockup-requirements-impact-review.md).

## 2. Tier 0 — Required technical foundation

This is not a separate learner-facing feature, but it is required before group activity and rewards are reliable.

- secure and de-duplicate lesson completion before it becomes reward-capable;
- course-instance-based learner scope;
- permission checks and explicit gamification permissions;
- configuration and rule versioning;
- unique source-occurrence identifiers;
- idempotent event processing;
- audit history for manual actions and corrections;
- challenge status and cancellation rules;
- privacy and access checks for Study Groups;
- seed or demonstration data.

Without this foundation, challenge contribution, XP, achievements, and results may be duplicated or become impossible to correct safely.

## 3. Tier 1 — Demonstrable MVP

### Course Progress integration

Initial scope:

- enable progress for one tracked Course Instance;
- calculate progress from unique trusted lesson completions;
- distinguish required, optional, and excluded lessons through new configuration;
- show progress and the next meaningful action in Course Details;
- keep progress separate from the LMS rule that records successful Course completion after all attached exams are passed.

### Study Groups

Initial scope:

- create or configure a Study Group for a course instance;
- join, request, invite, or staff-assign membership through at least one supported path;
- show members, roles, capacity, purpose, and status;
- restrict group access to members and authorized staff;
- leave, remove, close, or archive with basic audit information;
- no reward for joining, remaining, or communication volume.

### Collaborative Challenges

Initial scope:

- create or seed one reusable challenge definition;
- assign a challenge to a Study Group;
- show goal, requirements, availability, and current progress;
- record trusted individual contributions;
- show each learner's contribution eligibility;
- require a visible minimum personal contribution;
- complete the group challenge;
- support correction or cancellation;
- publish one group-completion event and eligible individual-contribution events.

### Limited supporting rewards

Initial scope:

- a small XP rule set connected to verified challenge events;
- one or two group or individual achievements;
- duplicate prevention;
- reward history and correction;
- no full reward catalogue or final artwork.

### Demonstration flow

The MVP should support this end-to-end scenario:

1. an enrolled learner views progress for a tracked Course Instance;
2. the learner joins or is assigned to a Study Group;
3. the group receives a Collaborative Challenge;
4. members complete different verified contributions;
5. group and individual progress update;
6. one member who did not meet the minimum is not given the same personal reward automatically;
7. the group completes the challenge;
8. eligible learners receive the configured XP or achievement once;
9. the result appears in Course Details or Profile.

## 4. Tier 2 — Exam journey and improved cooperative experience

Initial exam-journey scope may use confirmed mock-up data for:

- exam existence and type;
- learner enrollment;
- exam window and instructions;
- quiz results;
- practical submissions and results;
- pass/fail status;
- Certificate issuance after successful completion.

Final Exam Readiness still needs its own configurable checklist and must not infer attendance from enrollment, submission, or the exam date passing.

Possible cooperative additions:

- multiple active and completed challenges;
- temporary challenge teams;
- group organizer actions;
- challenge categories and filters;
- different contribution paths;
- group history;
- richer staff configuration;
- improved moderation and reporting;
- group-level achievements;
- notification integration for time-sensitive exam information.

These additions should follow the complete Tier 1 flow rather than replace it.

## 5. Tier 3 — Post-course Knowledge Refreshers

Initial scope:

- configure one refresher for a completed course;
- create eligibility after a configurable delay;
- show a short revision quiz or activity;
- store an attempt and result;
- show topic-level feedback;
- link to relevant completed material;
- publish a valid completion or result event;
- no penalty for missing or failing;
- no course-completion or certificate revocation;
- basic duplicate prevention and correction.

Reason: this directly supports long-term learning and provides a meaningful return path to the LMS. It is valuable but should not delay the complete Study Group and Collaborative Challenge MVP.

## 6. Tier 4 — Later variants and stretch features

### Optional Exploration Challenges

- optional practice or discovery activities;
- different contribution or solution paths;
- optional progress and achievements;
- no effect on required completion.

### Opt-in Competitive Challenges

- personal-best or team competition;
- explicit opt-in participation;
- fair scoring and tie rules;
- privacy controls;
- finalization before rewards;
- periodic reset or limited seasons.

Competition should begin only after cooperative challenge tracking is stable.

## 7. Future integration — not implemented in this project

### Skill Profile and Adaptive Learning Paths

The implementation may:

- tag Collaborative Challenges with skills;
- expose refresher results as possible skill evidence;
- accept future recommendation links.

The current scope does not include:

- a skill taxonomy;
- mastery calculations;
- recommendation ranking;
- diagnostic assessment design;
- automatic reduction of self-paced requirements;
- assessment-first course completion.

See [Future Skill Profile Integration](../06-integrations/future-skill-profile-integration.md).

## 8. Removed from the implementation sequence

The following initial ideas are no longer active implementation priorities:

- general Course Q&A and Peer Help;
- reaction-based or review-based Peer Contribution Recognition.

The reasons are documented in [Stakeholder Feedback and Scope Revision](../01-project-context/stakeholder-feedback-and-scope-revision.md).

Study Group communication may still be used to coordinate a defined learning activity. It should not become a second general-purpose technical Q&A platform.

## 9. Suggested implementation sequence

1. Secure lesson completion and define trusted event, audit, permission, correction, and configuration foundations.
2. Add Course Progress for one tracked Course Instance.
3. Add a basic Study Group model and learner view.
4. Implement one Study Group membership path.
5. Add a Collaborative Challenge definition and assignment.
6. Add individual contribution and shared progress.
7. Add completion, minimum-contribution eligibility, and corrections.
8. Integrate limited XP and one Achievement.
9. Add Final Exam Readiness from confirmed exam data.
10. Add Post-course Knowledge Refresher definition, eligibility, attempt, feedback, and review links.
11. Add an Optional Exploration or Opt-in Competitive variant only if time remains.

The implementation should remain modular so Study Groups, Collaborative Challenges, rewards, exam readiness, and refreshers can be selected independently during later integration.
