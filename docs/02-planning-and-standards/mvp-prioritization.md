# MVP Prioritization

> **Document status:** This is a rough release-planning outline revised after stakeholder review. Priorities may change after the LMS mock, technical discovery, implementation time, and available source data are confirmed.

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

See [Stakeholder Feedback and Scope Revision](../01-project-context/stakeholder-feedback-and-scope-revision.md).

## 2. Tier 0 — Required technical foundation

This is not a separate learner-facing feature, but it is required before group activity and rewards are reliable.

- course-instance-based learner scope;
- permission checks;
- configuration and rule versioning;
- unique source-occurrence identifiers;
- idempotent event processing;
- audit history for manual actions and corrections;
- challenge status and cancellation rules;
- privacy and access checks for Study Groups;
- seed or demonstration data.

Without this foundation, challenge contribution, XP, achievements, and results may be duplicated or become impossible to correct safely.

## 3. Tier 1 — Demonstrable MVP

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

1. an enrolled learner joins or is assigned to a Study Group;
2. the group receives a Collaborative Challenge;
3. members complete different verified contributions;
4. group and individual progress update;
5. one member who did not meet the minimum is not given the same personal reward automatically;
6. the group completes the challenge;
7. eligible learners receive the configured XP or achievement once.

## 4. Tier 2 — Improved cooperative experience

Possible additions:

- multiple active and completed challenges;
- temporary challenge teams;
- group organizer actions;
- challenge categories and filters;
- different contribution paths;
- group history;
- richer staff configuration;
- improved moderation and reporting;
- group-level achievements;
- optional integration with Course Progress, Course Milestones, and Final Exam Readiness.

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

1. Event, audit, permissions, and configuration foundation.
2. Basic Study Group model and learner view.
3. Study Group membership flow.
4. Collaborative Challenge definition and assignment.
5. Individual contribution and shared progress.
6. Completion, minimum-contribution eligibility, and corrections.
7. Limited XP and Achievement integration.
8. Post-course Knowledge Refresher definition and eligibility.
9. Refresher attempt, feedback, and review links.
10. Optional Exploration or Opt-in Competitive variant only if time remains.

The implementation should remain modular so Study Groups, Collaborative Challenges, rewards, and refreshers can be selected independently during later integration.
