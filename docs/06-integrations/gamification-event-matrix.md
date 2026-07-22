# Gamification Event Matrix

> **Document status:** This is a rough integration outline. Event names, payloads, transport, and ownership may change during technical design.

## 1. Purpose

This matrix shows which meaningful LMS or gamification events may feed progress, milestones, exam readiness, Study Groups, Collaborative Challenges, Post-course Knowledge Refreshers, XP, achievements, and future Skill Profile integration.

It is intended to prevent:

- rewarding the same action more than once by accident;
- allowing one feature to hard-code another feature's reward rules;
- assuming that data exists when the supplied LMS models do not confirm it;
- losing correction history when source results change.

A source feature should publish a trusted event once. Downstream features decide independently whether that event qualifies for progress, XP, an achievement, challenge progress, future skill evidence, or analytics.

## 2. Event rules

Every reward-capable or evidence-capable event should include, at minimum:

- a unique event or source-occurrence identifier;
- learner identifier where applicable;
- course and course-instance identifiers where applicable;
- group, challenge, refresher, or assessment identifiers where applicable;
- event type and occurrence time;
- trusted source or validating actor;
- rule or configuration version;
- correction or replacement relationship when data is changed.

Processing must be idempotent. Replaying the same source occurrence must not create duplicate progress, contribution, XP, achievements, refresher eligibility, or skill evidence.

## 3. Core learning and course events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `LEARNER_ENROLLED` | Existing LMS enrollment | Confirmed as data; event publishing may need implementation | Course Progress, Final Exam Readiness, Study Groups, analytics | Creates learner-course-instance scope; does not award XP by itself. |
| `REQUIRED_ACTIVITY_COMPLETED` | Existing LMS completion data or future activity service | Lesson completion is confirmed; other activity types are not | Course Progress, Collaborative Challenges, analytics | Must identify the unique required activity. |
| `REQUIRED_ACTIVITY_COMPLETION_REVOKED` | LMS correction or authorized staff | Requires correction workflow | Course Progress and downstream correction handling | Removes an invalid completion without deleting audit history. |
| `OPTIONAL_ACTIVITY_COMPLETED` | LMS or exploration feature | Requires optional-activity configuration | Course Progress, Optional Exploration Challenges | Must not affect required progress or exam eligibility unless separately configured. |
| `OPTIONAL_ACTIVITY_COMPLETION_REVOKED` | LMS correction or authorized staff | Requires correction workflow | Optional progress and downstream correction handling | Recalculates optional and combined progress. |
| `REQUIRED_PROGRESS_UPDATED` | Course Progress | New feature event | Course Milestones, Final Exam Readiness, analytics | Carries current required value from 0–100. |
| `OPTIONAL_PROGRESS_UPDATED` | Course Progress | New feature event | Course Milestones, Achievements, exploration analytics | Carries current optional value from 0–100. |
| `COURSE_COMPLETED` | Existing LMS course-completion source of truth | Course completion is confirmed as data; exact rule requires clarification | Course Milestones, XP, Achievements, Knowledge Refreshers, analytics | Means normal course-completion requirements are satisfied. |
| `COURSE_COMPLETION_REVOKED` | LMS correction or authorized staff | Requires correction workflow | Milestones, XP, Achievements, Knowledge Refreshers, analytics | May cancel unstarted refresher eligibility and correct rewards. |

## 4. Milestone and exam events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `MILESTONE_REACHED` | Course Milestones | New feature event | XP, Achievements, analytics | Payload identifies milestone type. |
| `EXAM_READINESS_UPDATED` | Final Exam Readiness | New feature event | Learner display, analytics, optional notification integration | Carries readiness status and completed or remaining requirements. |
| `EXAM_READY` | Final Exam Readiness | New feature event; depends on configured readiness data | Course Milestones, XP, Achievements, notification integration | Generated once when all active required readiness conditions are satisfied. |
| `EXAM_READY_REVOKED` | Final Exam Readiness correction | New feature event | XP, Achievements, notification integration | Used when corrected data means the learner is no longer ready. |
| `EXAM_REGISTRATION_AVAILABLE` | Exam or scheduling service | Not confirmed | Notification integration, learner display | Availability itself normally does not award XP. |
| `EXAM_ATTENDANCE_CONFIRMED` | Exam or attendance source | Not confirmed | Final Exam Readiness, Course Milestones, XP, Achievements, analytics | Must not be inferred from enrollment or the exam date passing. |
| `EXAM_COMPLETED` | Exam or assessment source | Not confirmed | Final Exam Readiness, Course Milestones, XP, Achievements, analytics | Completion and passing should remain distinct if tracked. |

## 5. Study Group events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `STUDY_GROUP_CREATED` | Study Groups | Requires new group feature | Administration and analytics | Creation does not award XP. |
| `STUDY_GROUP_MEMBERSHIP_CHANGED` | Study Groups | Requires new group feature | Access control, Collaborative Challenges, analytics | Joining, remaining, or leaving does not award XP. |
| `STUDY_GROUP_ROLE_CHANGED` | Study Groups | Requires new group feature | Access control and audit | A role change does not prove learning contribution. |
| `STUDY_GROUP_ARCHIVED` | Study Groups | Requires new group feature | Access control, challenge administration | Archived groups are normally read-only. |

## 6. Collaborative Challenge events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `COLLABORATIVE_CHALLENGE_ASSIGNED` | Collaborative Challenges | Requires new challenge feature | Group display and analytics | Assignment does not award XP. |
| `COLLABORATIVE_CHALLENGE_STARTED` | Collaborative Challenges | Requires new challenge feature | Group display and analytics | Records availability or accepted participation. |
| `COLLABORATIVE_CONTRIBUTION_CONFIRMED` | Collaborative Challenges | Requires new challenge feature | Challenge progress, XP, Achievements, optional Skill Profile integration | Must identify the learner's verified contribution and source occurrence. |
| `COLLABORATIVE_CHALLENGE_PROGRESS_UPDATED` | Collaborative Challenges | Requires new challenge feature | Group display and analytics | Carries shared progress and remaining requirements. |
| `COLLABORATIVE_CHALLENGE_COMPLETED` | Collaborative Challenges | Requires new challenge feature | XP, Achievements, analytics | Group completion and individual reward eligibility remain separate. |
| `COLLABORATIVE_CONTRIBUTION_REVOKED` | Challenge correction | Requires new challenge feature | Challenge progress, XP and Achievement corrections, optional Skill Profile correction | Identifies the original contribution occurrence. |
| `COLLABORATIVE_CHALLENGE_CANCELLED` | Collaborative Challenges | Requires new challenge feature | Group display, analytics, reward prevention | Cancellation must include a reason and must not appear as learner failure. |

## 7. Post-course Knowledge Refresher events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `KNOWLEDGE_REFRESHER_ELIGIBLE` | Post-course Knowledge Refreshers | Requires new refresher feature | Learner display and optional notification integration | Created after trusted course completion and configured delay. |
| `KNOWLEDGE_REFRESHER_STARTED` | Post-course Knowledge Refreshers | Requires new refresher feature | Attempt history and analytics | Starting alone normally does not award XP. |
| `KNOWLEDGE_REFRESHER_COMPLETED` | Post-course Knowledge Refreshers | Requires new refresher feature | XP, Achievements, analytics, optional Skill Profile integration | Carries result summary and definition version. |
| `KNOWLEDGE_REFRESHER_REVIEW_RECOMMENDED` | Post-course Knowledge Refreshers | Requires topic-level evaluation | Learner display, review-link recommendations | Must not revoke course completion. |
| `KNOWLEDGE_REFRESHER_RESULT_CORRECTED` | Refresher correction | Requires new refresher feature | XP and Achievement corrections, optional Skill Profile correction | Preserves the original result in audit history. |

## 8. Optional and competitive challenge events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `EXPLORATION_CHALLENGE_COMPLETED` | Optional Exploration Challenges | Requires new challenge feature | Optional progress, XP, Achievements | Must not affect required course completion. |
| `EXPLORATION_CHALLENGE_COMPLETION_REVOKED` | Exploration correction | Requires new challenge feature | Optional progress and reward corrections | Recalculates optional progress and downstream rewards. |
| `COMPETITIVE_CHALLENGE_COMPLETED` | Opt-in Competitive Challenges | Requires new competitive feature | XP, Achievements, analytics | Participation must be opt-in. |
| `COMPETITIVE_POSITION_CONFIRMED` | Opt-in Competitive Challenges | Requires new competitive feature | Achievements and optional XP | Generated only after scores and ties are finalized. |
| `PERSONAL_BEST_IMPROVED` | Opt-in Competitive Challenges | Requires new competitive feature | XP, Achievements, analytics | Supports comparison against the learner's own result. |
| `COMPETITIVE_RESULT_REVOKED` | Competitive correction | Requires new competitive feature | XP and Achievement corrections | Used after invalid score or ranking correction. |

## 9. Reward events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `XP_AWARDED` | Meaningful XP and Levels | New feature event | Learner XP display, analytics | Created from a trusted source event and XP rule; does not feed course progress. |
| `XP_REVERSED` | Meaningful XP and Levels | New feature event | Learner XP display, analytics | Reversing transaction preserves the original award. |
| `LEVEL_REACHED` | Meaningful XP and Levels | New feature event | Achievements and learner display | Does not grant academic credit or exam eligibility. |
| `ACHIEVEMENT_AWARDED` | Achievements and Badges | New feature event | Learner display and analytics | A badge should not automatically add duplicate XP for the same source event. |
| `ACHIEVEMENT_REVOKED` | Achievements and Badges | New feature event | Learner display and analytics | Revocation remains auditable. |

## 10. Future Skill Profile integration events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `SKILL_EVIDENCE_AVAILABLE` | Challenge, refresher, or assessment adapter | Future integration | Skill Profile | Must distinguish practice, completion, assessment, and verified mastery. |
| `SKILL_EVIDENCE_REVOKED` | Source correction adapter | Future integration | Skill Profile | Identifies the original evidence occurrence. |
| `COURSE_RECOMMENDATION_AVAILABLE` | Future recommendation service | Future integration | Learner display | Should include an understandable reason. |

These events do not imply that a Skill Profile is implemented in the current project.

## 11. Initial source availability summary

### Available or partly available from the supplied LMS models

- learner enrollment in courses and course instances;
- completed course lessons;
- course-completion records;
- course and course-instance type, including live and self-paced delivery;
- programs and certificates.

These records may still require a new event-publishing or change-detection layer.

### Not confirmed and requiring new tracking or integration

- required versus optional activity configuration;
- final-exam eligibility, registration, attendance, completion, and passing;
- live-session attendance;
- Study Groups, membership, roles, and group communication;
- Collaborative Challenge definitions, contributions, and results;
- Post-course Knowledge Refresher definitions, schedules, attempts, and results;
- detailed assessment outcomes;
- skill taxonomy, mastery, and recommendation data.

## 12. Implementation boundary

The event matrix does not define exact payload schemas, queues, APIs, database models, XP amounts, badge conditions, question formats, or skill calculations. Those decisions belong to technical design if implementation is approved.
