# Study Groups

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Study Groups allows learners in the same course instance to form or join small groups for discussion, practice, mutual support, and final-exam preparation.

A study group provides membership and a defined learning purpose. It is separate from a Collaborative Challenge: a group may exist without a challenge, and a challenge may later be assigned to one or more groups.

A group should include:

- name and purpose;
- related course instance;
- members and group roles;
- membership capacity and joining policy;
- active, archived, or closed status;
- optional reference to a course stage or exam-preparation period;
- access to an approved group communication space or integration.

Learners may join voluntarily where allowed. Course managers may also create or assign groups when structured collaboration is required.

Joining a group does not itself award XP, progress, or an achievement.

## 2. Why

Learners may disengage because they feel isolated or have difficulty recovering after falling behind. Small groups create a manageable community for asking questions, sharing understanding, and preparing together.

The feature supports:

- meaningful communication outside lessons;
- peer support and belonging;
- exam preparation;
- help for learners who are stuck or behind;
- a foundation for collaborative challenges.

The group must support learning rather than require unnecessary daily website activity.

## 3. How

### 3.1 Group scope

A study group belongs to one course instance by default. This keeps membership relevant to the same course delivery, schedule, and final exam.

A group may be:

- learner-created with course-manager permission;
- staff-created and open for voluntary joining;
- staff-assigned for a structured activity;
- private to members while still visible to authorized course staff.

Program-wide or cross-course groups are outside the first version.

### 3.2 Membership

Each group should define:

- minimum and maximum size;
- open, request-to-join, invitation-only, or assigned membership;
- whether learners may leave freely;
- whether a replacement may join;
- member, group organizer, and staff moderator roles.

A learner may belong to more than one group only when the course configuration allows it. The first version should normally limit a learner to one general study group per course instance to reduce fragmentation, while allowing temporary challenge teams separately.

### 3.3 Group creation and lifecycle

Authorized users should be able to:

- create a group with a clear learning purpose;
- join, invite, approve, remove, or leave according to policy;
- archive a group after the course or preparation period;
- close a group that is inactive, abusive, or no longer relevant;
- transfer organizer responsibilities when needed.

Archived groups become read-only unless course policy requires deletion.

### 3.4 Group activity and recognition

The group may use a dedicated discussion area or a supported communication integration. The communication mechanism must preserve course and group access controls.

No reward is given for:

- joining a group;
- remaining a member;
- sending a message;
- daily attendance in the group space;
- inviting many learners.

Recognition may come only from a separate validated action, such as an accepted solution, approved study resource, completed group task, or collaborative challenge contribution.

### 3.5 Staff oversight and safety

Authorized course staff should be able to view group membership and intervene when necessary.

Learners should be able to report inappropriate content or behavior. Removal from a group should not remove course enrollment.

Detailed group communication should remain visible only to members and authorized staff, subject to the institution’s moderation and retention policy.

## 4. Motivation types supported

- **Socializers — strong:** belonging, communication, and mutual support.
- **Achievers — medium:** groups can support preparation and completion goals.
- **Explorers — medium:** learners may share resources and alternative explanations.
- **Competitors — low to medium:** competition is not required, but groups may later join opt-in team challenges.

## 5. Live-course behavior

- Groups may align with scheduled cohorts, lesson times, or exam-preparation periods.
- Learners are not required to interact daily between lessons.
- Late-enrolling learners may join an open group with capacity or be assigned appropriately.
- Cancelled or rescheduled lessons do not automatically change group membership.
- Groups may remain active until the final exam or configured course end.

## 6. Self-paced-course behavior

- Groups should use broad progress stages or topics rather than assuming all members are on the same lesson.
- Learners may join groups compatible with their current stage where available.
- Taking a break does not automatically remove membership.
- Staff may archive inactive groups or offer movement to a more active group.
- Fixed meeting expectations must be clearly communicated and optional unless the course explicitly requires them.

## 7. Rules and edge cases

- Joining or creating a group does not award XP.
- Group membership does not change course progress or exam eligibility.
- A learner removed from a group remains enrolled in the course.
- A learner who leaves a group keeps valid previously earned recognition but loses access to future private group activity.
- Staff may move learners to balance group size, with appropriate communication and audit history.
- Empty or inactive groups may be archived.
- A group organizer cannot remove authorized course staff.
- Group rewards must use validated contributions or challenge rules, not equal rewards merely for membership.
- Public group membership should not be exposed outside the course by default.
- Group communication notifications are outside the current feature scope.

## 8. Acceptance criteria

### AC1 — Create a group

Given an authorized learner or staff member may create study groups for a course instance,
when they provide the required name, purpose, capacity, and joining policy,
then an Active group is created for that course instance.

### AC2 — Join an open group

Given a learner is enrolled in the course instance
and an open group has available capacity,
when the learner joins,
then they become a member and gain access to the group space.

### AC3 — Capacity limit

Given a study group has reached its configured maximum size,
when another learner attempts to join,
then the system prevents the membership unless authorized staff increases capacity or removes a member.

### AC4 — No joining reward

Given a learner joins, remains in, or creates a study group,
when membership is processed,
then no XP, achievement, or course progress is awarded solely for that action.

### AC5 — Leave group

Given a learner voluntarily leaves a group,
when the change is processed,
then they lose access to future private group activity
but remain enrolled in the course and keep valid prior recognition.

### AC6 — Staff oversight

Given a learner reports a group or member,
when authorized staff reviews the report,
then they may record a decision, remove content or membership, or close the group with an auditable reason.

### AC7 — Late enrollment

Given a learner joins a live course after it has started,
when an eligible group has capacity,
then the learner may join or be assigned without receiving automatic credit for earlier group activity.

### AC8 — Archive

Given a course or preparation period has ended,
when authorized staff archives the group,
then the group becomes read-only and no new activity or membership is accepted.

## 9. Required LMS data

### Confirmed from the supplied models

- users;
- courses and course instances;
- learner enrollment;
- live and self-paced course types.

### New data required

- study-group definitions and membership;
- group roles and joining requests or invitations;
- group status and audit history;
- group communication space or integration;
- reporting and moderation records.

## 10. Model extensions

The supplied LMS models should not be modified.

### `StudyGroup`

Stores the course instance, name, purpose, capacity, joining policy, status, organizer, optional course-stage context, and timestamps.

### `StudyGroupMembership`

Stores the group, learner, role, membership status, joining method, joined and left times, and relevant audit information.

### `StudyGroupJoinRequest`

Stores request or invitation information when the group is not open joining.

### `StudyGroupAuditEvent`

Stores creation, role changes, removals, closure, archiving, staff actions, and reasons.

## 11. Success measure

Useful indicators include:

- percentage of learners voluntarily joining or remaining in an active group;
- percentage of groups with meaningful learning activity;
- learners receiving or providing validated help through groups;
- progress, exam-readiness, attendance, and completion rates of participating learners compared carefully with similar non-participants;
- group inactivity, removal, report, and closure rates;
- learner feedback on usefulness and belonging.

Message volume and daily visits are not success measures by themselves.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
