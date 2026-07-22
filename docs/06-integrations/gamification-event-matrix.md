# Gamification Event Matrix

> **Document status:** Rough integration outline grounded in the full LMS mock-up. Event names, payloads, transport, and ownership remain provisional.

## 1. Purpose

One trusted source occurrence may feed Course Progress, Milestones, Exam Readiness, Study Groups, Collaborative Challenges, Knowledge Refreshers, XP, Achievements, analytics, or future Skill Profile integration. Each consumer decides independently what the occurrence means.

The matrix prevents duplicate rewards, hidden coupling, and unsupported assumptions.

## 2. Event contract

Every reward/evidence-capable event should include:

- globally unique occurrence ID;
- event type;
- learner and actor IDs where applicable;
- Course, Course Instance, lesson, Assessment, Program, Certificate, group, or challenge IDs where applicable;
- occurrence and recorded times;
- source service and trust level;
- source/rule version;
- correction/replacement reference;
- minimum payload needed to re-evaluate the rule.

All consumers must be idempotent by occurrence ID. Mirrored writes may publish only one logical event.

## 3. Existing LMS and learning events

| Proposed event | Current source | Availability | Main consumers | Notes |
|---|---|---|---|---|
| `LEARNER_ENROLLED` | Course/Seminar Instance enrollment service | Confirmed data; adapter required | Progress scope, Groups, analytics | No XP for enrollment alone. Self-identity hardening is recommended on Course enrollment. |
| `LESSON_COMPLETED` | Course Instance lesson `completedBy` | Data exists; source not trusted for rewards yet | Course Progress | Harden identity, enrollment, rules, and uniqueness first. |
| `LESSON_COMPLETION_REVOKED` | New correction workflow | Not implemented | Progress and reward corrections | Preserve original occurrence. |
| `ASSESSMENT_STARTED` | Assessment result timestamps | Partly available | Analytics, attempt history | Starting alone normally gives no XP. |
| `ASSESSMENT_COMPLETED` | `Assessment.results.completedAt` / result service | Confirmed | Progress, Challenges, analytics | Identify assessment type and unique attempt. |
| `ASSESSMENT_PASSED` | Result score compared with stored pass score | Confirmed | Readiness, Milestones, Challenges, XP/Achievements by rule | Keep pass threshold snapshot. |
| `ASSESSMENT_NOT_PASSED` | Result below pass score | Confirmed | Readiness, feedback, analytics | Should not remove prior valid evidence without correction semantics. |
| `ASSESSMENT_RESULT_CORRECTED` | Staff result update/import | Result editing exists; event/audit extension required | Readiness, completion, rewards | Reference prior result occurrence. |
| `EXAM_ENROLLED` | `Assessment.examEnrolledUsers` | Confirmed | Readiness, learner display | Enrollment is access state, not attendance or XP. |
| `EXAM_WINDOW_OPENED` | Exam schedule adapter | Derivable from confirmed dates | Readiness, notifications | Scheduled state event; no reward. |
| `EXAM_WINDOW_CLOSED` | Exam schedule adapter | Derivable from confirmed dates | Readiness, notifications | Does not prove attempt/attendance. |
| `PRACTICAL_SUBMISSION_RECORDED` | Practical submission service | Confirmed | Readiness, Challenge if explicitly configured | Proves a file submission, not quality or pass. Re-upload should replace, not multiply credit. |
| `PRACTICAL_SUBMISSION_REPLACED` | Practical re-upload | Confirmed behavior; adapter required | Audit, readiness | Normally no extra progress or XP. |
| `COURSE_COMPLETED` | User service after all Course Instance exams pass | Confirmed business rule; adapter required | Milestones, XP, Achievements, Refreshers, analytics | Logical event should carry Course and source Course Instance. |
| `COURSE_COMPLETION_REVOKED` | New correction/recalculation workflow | Not implemented | Downstream corrections | Current mirrored arrays do not express revocation history. |
| `CERTIFICATE_ISSUED` | Administrator certificate service | Confirmed | XP, Achievements, analytics | Strong event; separate from Course completion. |
| `CERTIFICATE_UPDATED_OR_REISSUED` | Certificate service | Confirmed update behavior; adapter required | Audit, learner display | Do not award the original achievement twice. |
| `PROGRAM_PROGRESS_UPDATED` | Program calculation | Confirmed derived state | Milestones, analytics | Publish threshold crossing rather than repeated reads. |
| `PROGRAM_COMPLETED` | Program completion workflow | Confirmed | XP, Achievements, analytics | Idempotent by learner + Program completion occurrence. |

## 4. Progress and readiness events

| Proposed event | Owner | Availability | Main consumers | Notes |
|---|---|---|---|---|
| `REQUIRED_PROGRESS_UPDATED` | Course Progress | New | Milestones, Readiness, analytics | Carries 0–100 and requirement version. |
| `OPTIONAL_PROGRESS_UPDATED` | Course Progress | New | Achievements, exploration analytics | Does not complete the Course. |
| `COURSE_PROGRESS_RECALCULATED` | Course Progress | New | Learner display, audit | May increase or decrease after correction. |
| `MILESTONE_REACHED` | Course Milestones | New | XP, Achievements, analytics | One event per milestone/version. |
| `MILESTONE_REVOKED` | Course Milestones | New | Reward corrections | Used after source correction. |
| `EXAM_READINESS_UPDATED` | Final Exam Readiness | New | Learner display, analytics | Carries checklist counts and next action. |
| `EXAM_READY` | Final Exam Readiness | New | Milestones, XP/Achievements by rule, notification adapter | Means configured readiness only. |
| `EXAM_READY_REVOKED` | Final Exam Readiness | New | Corrections, notifications | Auditable correction. |
| `EXAM_ATTENDANCE_CONFIRMED` | Future attendance source | Unavailable | Milestones, analytics | Must not be inferred from enrollment/window/result. |

## 5. Study Group events

| Proposed event | Owner | Availability | Main consumers | Notes |
|---|---|---|---|---|
| `STUDY_GROUP_CREATED` | Study Groups | New | Administration, analytics | No reward. |
| `STUDY_GROUP_MEMBERSHIP_CHANGED` | Study Groups | New | Access control, Challenges, analytics | Joining/leaving gives no XP. |
| `STUDY_GROUP_ROLE_CHANGED` | Study Groups | New | Access control, audit | No reward. |
| `STUDY_GROUP_ARCHIVED` | Study Groups | New | Access control, challenge administration | Normally read-only afterward. |
| `STUDY_GROUP_MODERATION_ACTION_RECORDED` | Study Groups | New | Safety/audit | Never a learner reward source. |

## 6. Collaborative Challenge events

| Proposed event | Owner | Availability | Main consumers | Notes |
|---|---|---|---|---|
| `COLLABORATIVE_CHALLENGE_ASSIGNED` | Collaborative Challenges | New | Group display, analytics | No reward for assignment/joining. |
| `COLLABORATIVE_CHALLENGE_STARTED` | Collaborative Challenges | New | Display, analytics | Records availability. |
| `COLLABORATIVE_CONTRIBUTION_CONFIRMED` | Collaborative Challenges | New | Progress, XP, Achievements, future skills | Must identify validator/source and unique contribution. |
| `COLLABORATIVE_CONTRIBUTION_REVOKED` | Challenge correction | New | Progress and reward corrections | Reference original contribution. |
| `COLLABORATIVE_CHALLENGE_PROGRESS_UPDATED` | Collaborative Challenges | New | Group display, analytics | Shared progress only. |
| `COLLABORATIVE_CHALLENGE_COMPLETED` | Collaborative Challenges | New | XP/Achievements by rule, analytics | Team completion and personal eligibility remain separate. |
| `COLLABORATIVE_CHALLENGE_CANCELLED` | Collaborative Challenges | New | Display, reward prevention, analytics | Show cancellation, not learner failure. |

## 7. Post-course Knowledge Refresher events

| Proposed event | Owner | Availability | Main consumers | Notes |
|---|---|---|---|---|
| `KNOWLEDGE_REFRESHER_ELIGIBLE` | Knowledge Refreshers | New | Learner display, notifications | Based on trusted Course completion and delay. |
| `KNOWLEDGE_REFRESHER_STARTED` | Knowledge Refreshers | New | Attempt history, analytics | No reward for starting. |
| `KNOWLEDGE_REFRESHER_COMPLETED` | Knowledge Refreshers | New | XP, Achievements, analytics, future skills | Assessment engine concepts may be reused, but this is a separate feature/version. |
| `KNOWLEDGE_REFRESHER_REVIEW_RECOMMENDED` | Knowledge Refreshers | New | Learner display | Topic-level result and Course-material links required. |
| `KNOWLEDGE_REFRESHER_RESULT_CORRECTED` | Refresher correction | New | Reward/skill corrections | Preserve original result. |

## 8. Optional and competitive events

| Proposed event | Owner | Availability | Main consumers | Notes |
|---|---|---|---|---|
| `EXPLORATION_CHALLENGE_COMPLETED` | Optional Exploration Challenges | Later/new | Optional progress, XP, Achievements | Never required Course progress unless separately configured. |
| `EXPLORATION_CHALLENGE_COMPLETION_REVOKED` | Exploration correction | Later/new | Corrections | Recalculate optional progress. |
| `COMPETITIVE_CHALLENGE_COMPLETED` | Opt-in Competitive Challenges | Later/new | XP, Achievements, analytics | Participation is opt-in. |
| `COMPETITIVE_POSITION_CONFIRMED` | Competitive Challenges | Later/new | Achievements, optional XP | Only after finalized score/ties. |
| `PERSONAL_BEST_IMPROVED` | Competitive Challenges | Later/new | XP, Achievements, analytics | Supports self-comparison. |
| `COMPETITIVE_RESULT_REVOKED` | Competitive correction | Later/new | Reward corrections | Auditable invalidation. |

## 9. Reward events

| Proposed event | Owner | Availability | Main consumers | Notes |
|---|---|---|---|---|
| `XP_AWARDED` | XP and Levels | New | Learner display, analytics | References one trusted source occurrence and rule version. |
| `XP_REVERSED` | XP and Levels | New | Learner display, analytics | Reversal transaction preserves original award. |
| `LEVEL_REACHED` | XP and Levels | New | Achievements, display | No academic credit. |
| `ACHIEVEMENT_AWARDED` | Achievements | New | Learner display, analytics | Must not duplicate XP for same source by accident. |
| `ACHIEVEMENT_REVOKED` | Achievements | New | Learner display, analytics | Auditable. |

## 10. Explicit non-events

The following must not generate reward-capable learning events by themselves:

- login or token refresh;
- opening a page or lesson;
- remaining online;
- payment or discount use;
- Course/Exam enrollment alone;
- joining or messaging in a Study Group;
- the random client-side Activity Tracker value;
- exam date passing;
- unverified message/reaction counts.

## 11. Initial integration order

1. Harden and normalize lesson completion.
2. Add a durable source-event/outbox adapter.
3. Publish assessment pass, practical submission, Course completion, Certificate, and Program events.
4. Implement Course Progress and Readiness consumers.
5. Add Study Group/Challenge source events.
6. Add XP/Achievement consumers with reversal support.
7. Add Refresher and later challenge events.
