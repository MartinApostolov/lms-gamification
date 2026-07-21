# Gamification Event Matrix

> **Document status:** This is a rough integration outline. Event names, payloads, transport, and ownership may change during technical design.

## 1. Purpose

This matrix shows which meaningful LMS or gamification events may feed progress, milestones, exam readiness, XP, achievements, recognition, and challenges.

It is intended to prevent three common problems:

- rewarding the same action more than once by accident;
- allowing one feature to hard-code another feature's reward rules;
- assuming that data exists when the supplied LMS models do not confirm it.

A source feature should publish a trusted event once. Downstream features decide independently whether that event qualifies for progress, XP, an achievement, a challenge score, or analytics.

## 2. Event rules

Every reward-capable event should include, at minimum:

- a unique event or source-occurrence identifier;
- learner identifier;
- course and course-instance identifiers when applicable;
- event type and occurred time;
- trusted source or validating actor;
- rule or configuration version where relevant;
- correction or replacement relationship when data is changed.

Processing must be idempotent. Replaying the same source occurrence must not create duplicate progress, XP, achievements, recognition, or challenge score.

## 3. Core learning and course events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `LEARNER_ENROLLED` | Existing LMS enrollment | Confirmed as data; event publishing may need implementation | Course Progress, Final Exam Readiness, analytics | Creates learner-course-instance scope; does not award XP by itself. |
| `REQUIRED_ACTIVITY_COMPLETED` | Existing LMS completion data or future activity service | Lesson completion is confirmed; other activity types are not | Course Progress, challenges, analytics | Must identify the unique required activity. |
| `REQUIRED_ACTIVITY_COMPLETION_REVOKED` | LMS correction or authorized staff | Requires correction workflow | Course Progress and downstream correction handling | Removes an invalid completion without deleting audit history. |
| `OPTIONAL_ACTIVITY_COMPLETED` | LMS or exploration feature | Requires optional-activity configuration | Course Progress, exploration challenges | Must not affect required progress or exam eligibility unless separately configured. |
| `OPTIONAL_ACTIVITY_COMPLETION_REVOKED` | LMS correction or authorized staff | Requires correction workflow | Course Progress and downstream correction handling | Recalculates optional and combined progress. |
| `REQUIRED_PROGRESS_UPDATED` | Course Progress | New feature event | Course Milestones, Final Exam Readiness, analytics | Carries current required value from 0–100. |
| `OPTIONAL_PROGRESS_UPDATED` | Course Progress | New feature event | Course Milestones, Achievements, exploration analytics | Carries current optional value from 0–100. |
| `COURSE_PROGRESS_RECALCULATED` | Course Progress | New feature event | Audit and analytics | Useful when course rules change without a learner action. |
| `COURSE_COMPLETED` | Existing LMS course-completion source of truth | Course completion is confirmed as data; exact rule requires clarification | Course Milestones, XP, Achievements, analytics | Means normal course-completion requirements are satisfied; optional 100% is not required. |
| `COURSE_COMPLETION_REVOKED` | LMS correction or authorized staff | Requires correction workflow | Milestones, XP, Achievements, analytics | Used only when an existing completion is invalidated. |

## 4. Milestone and exam events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `MILESTONE_REACHED` | Course Milestones | New feature event | XP, Achievements, analytics | Payload identifies milestone type, such as Course Started, Halfway, Required Work Complete, or All Activities Complete. |
| `EXAM_READINESS_UPDATED` | Final Exam Readiness | New feature event | Learner display, analytics, optional notification integration | Carries readiness status and completed/remaining requirements. |
| `EXAM_READY` | Final Exam Readiness | New feature event; depends on configured readiness data | Course Milestones, XP, Achievements, notification integration | Generated once when all active required readiness conditions are satisfied. |
| `EXAM_READY_REVOKED` | Final Exam Readiness correction | New feature event | XP, Achievements, notification integration | Used when corrected data means the learner is no longer ready. |
| `EXAM_REGISTRATION_AVAILABLE` | Exam or scheduling service | Not confirmed | Notification integration, learner display | Availability itself normally does not award XP. |
| `EXAM_ATTENDANCE_CONFIRMED` | Exam or attendance source | Not confirmed | Final Exam Readiness, Course Milestones, XP, Achievements, analytics | Must not be inferred from enrollment or the exam date passing. |
| `EXAM_COMPLETED` | Exam or assessment source | Not confirmed | Final Exam Readiness, Course Milestones, XP, Achievements, analytics | Completion and passing should remain distinct if the LMS tracks both. |

## 5. Q&A and peer-contribution events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `QUESTION_CREATED` | Course Q&A and Peer Help | Requires new communication feature | Analytics only by default | Creating a question does not award XP. |
| `ANSWER_CREATED` | Course Q&A and Peer Help | Requires new communication feature | Activity history and analytics only by default | Creating an answer does not award XP by itself. |
| `ANSWER_ACCEPTED` | Course Q&A and Peer Help | Requires new communication feature | Peer Contribution Recognition | Trusted validation event; asker or authorized staff accepts one solution. |
| `ANSWER_UNACCEPTED` | Course Q&A and Peer Help | Requires new communication feature | Peer Contribution Recognition correction | Removes active accepted-solution status. |
| `CONTENT_REMOVED` | Q&A moderation | Requires new communication feature | Peer Contribution Recognition correction | Used when a rewarded answer is deleted or moderated. |
| `CONTRIBUTION_RECOGNIZED` | Peer Contribution Recognition | New feature event | XP, Achievements, challenge eligibility, analytics | Indicates validated useful contribution, not raw message volume. |
| `CONTRIBUTION_REVOKED` | Peer Contribution Recognition | New feature event | XP and Achievement corrections | Preserves audit history while removing active recognition. |

## 6. Group and challenge events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `STUDY_GROUP_CREATED` | Study Groups | Requires new group feature | Analytics and administration | Group creation does not award XP by itself. |
| `STUDY_GROUP_MEMBERSHIP_CHANGED` | Study Groups | Requires new group feature | Access control, collaborative challenges | Joining, remaining, or leaving does not award XP by itself. |
| `COLLABORATIVE_CONTRIBUTION_CONFIRMED` | Collaborative Challenges | Requires new challenge feature | Peer Contribution Recognition, challenge progress | Must identify the learner's verified individual contribution. |
| `COLLABORATIVE_CHALLENGE_COMPLETED` | Collaborative Challenges | Requires new challenge feature | XP, Achievements, analytics | Team completion and individual reward eligibility remain separate. |
| `COLLABORATIVE_CONTRIBUTION_REVOKED` | Collaborative Challenges correction | Requires new challenge feature | Recognition, XP, Achievement corrections | Replaces the earlier idea of a challenge feature directly revoking rewards. |
| `EXPLORATION_CHALLENGE_COMPLETED` | Optional Exploration Challenges | Requires new challenge feature | Course Progress optional score, XP, Achievements | Must not affect required course completion. |
| `EXPLORATION_CHALLENGE_COMPLETION_REVOKED` | Exploration correction | Requires new challenge feature | Course Progress and reward corrections | Recalculates optional progress and downstream rewards. |
| `COMPETITIVE_CHALLENGE_COMPLETED` | Opt-in Competitive Challenges | Requires new competitive feature | XP, Achievements, analytics | Participation must be opt-in. |
| `COMPETITIVE_POSITION_CONFIRMED` | Opt-in Competitive Challenges | Requires new competitive feature | Achievements and optional XP | Generated only after scores and ties are finalized. |
| `PERSONAL_BEST_IMPROVED` | Opt-in Competitive Challenges | Requires new competitive feature | XP, Achievements, analytics | Supports comparison against the learner's own result. |
| `COMPETITIVE_RESULT_REVOKED` | Competitive correction | Requires new competitive feature | XP and Achievement corrections | Used after invalid score or ranking correction. |

## 7. Reward events

| Proposed event | Owner or source | Current availability | Main consumers | Notes |
|---|---|---|---|---|
| `XP_AWARDED` | Meaningful XP and Levels | New feature event | Learner XP display, analytics | Created from a trusted source event and XP rule; does not feed course progress. |
| `XP_REVERSED` | Meaningful XP and Levels | New feature event | Learner XP display, analytics | Reversing transaction preserves the original award. |
| `LEVEL_REACHED` | Meaningful XP and Levels | New feature event | Achievements and learner display | Does not grant academic credit or exam eligibility. |
| `ACHIEVEMENT_AWARDED` | Achievements and Badges | New feature event | Learner display and analytics | Badge award should not automatically add extra XP for the same source event unless explicitly intended. |
| `ACHIEVEMENT_REVOKED` | Achievements and Badges | New feature event | Learner display and analytics | Revocation remains auditable. |

## 8. Initial source availability summary

### Available or partly available from the supplied LMS models

- learner enrollment in courses and course instances;
- completed lessons;
- course-completion records;
- course and course-instance type, including live and self-paced delivery;
- programs and certificates.

These records may still require a new event-publishing or change-detection layer.

### Not confirmed and requiring new tracking or integration

- required versus optional activity configuration;
- final-exam eligibility, registration, attendance, completion, and passing;
- live-session attendance;
- questions, answers, comments, accepted solutions, and moderation;
- peer-contribution validation;
- study groups;
- collaborative, exploration, and competitive challenges;
- detailed assessment outcomes.

## 9. Implementation boundary

The event matrix does not define exact payload schemas, queues, APIs, database models, XP amounts, or badge conditions. Those decisions belong to technical design if implementation is approved.
