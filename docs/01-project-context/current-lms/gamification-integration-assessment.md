# Gamification Integration Assessment

## 1. Capability classification

### Reusable now through a trusted adapter

- authenticated users and exact roles;
- Course, Course Instance, and live/self-paced scope;
- assessment attempts and completion;
- quiz/practical scores and pass thresholds;
- exam enrollment and access windows;
- practical-exam submission occurrence;
- successful Course completion after all attached exams are passed;
- Program progress and completion;
- Certificate issuance and final certificate score;
- User privacy setting.

### Reusable after hardening or configuration

- Course lesson completion — requires identity, enrollment, business-rule, and idempotency hardening;
- Course/Seminar enrollment routes that accept a target user ID — require consistent owner/staff authorization;
- required and optional progress — requires an explicit requirement classification;
- staff result corrections — should preserve audit and publish correction events;
- Survey participation — schema is flexible and no active main route was found.

### Must be added

- Study Group, membership, join/leave/invite, roles, lifecycle, communication link, reporting, and moderation;
- Collaborative Challenge definitions, instances, teams, verified contributions, progress, completion, and cancellation;
- XP ledger, levels, rule versions, caps, and reversals;
- achievement definitions and learner awards;
- Post-course Knowledge Refresher scheduling, eligibility, topic mapping, attempts, feedback, and review links;
- final-exam readiness configuration and learner checklist state;
- optional/competitive challenge infrastructure;
- notification preferences for new gamification events.

### Still unavailable and must not be inferred

- live-class attendance or punctuality;
- seminar completion;
- learning time spent;
- reliable daily activity streaks;
- message quality from message volume;
- contribution merely from group membership;
- exam attendance from enrollment or the exam date passing.

## 2. Requirement-by-requirement fit

| Requirement area | Fit with current mock-up | Required change |
|---|---|---|
| Course Progress | Partial | Use tracked lessons; add requirement classification and secure idempotent completion |
| Course Milestones | Partial | Derive from de-duplicated progress, exam readiness, completion, and certificate events |
| Final Exam Readiness | Stronger than first assumed | Configure checklist around existing exams/results/windows; add readiness state and manual evidence audit |
| Meaningful XP and Levels | No current model | Add ledger/rules; consume trusted events only |
| Achievements and Badges | No current model | Add definitions/awards; Course completion and Certificate are strongest initial sources |
| Study Groups | No current model/UI/API | Add course-instance-scoped feature and staff/learner screens |
| Collaborative Challenges | No current model/UI/API | Add separate challenge framework and verified contribution evidence |
| Knowledge Refreshers | Partial engine reuse possible | Reuse/adapt assessment concepts but add post-course scheduling, topic feedback, versioning, and review links |
| Exploration Challenges | No current framework | Later extension; keep optional progress separate |
| Competitive Challenges | No current framework | Later opt-in feature with privacy and fairness controls |

## 3. Recommended MVP implementation seam

A low-risk demonstration can be built around one seeded tracked Course Instance:

1. show de-duplicated required lesson progress;
2. show existing attached exam state and a readiness checklist;
3. create one Study Group for enrolled learners;
4. assign one Collaborative Challenge with explicit verified contribution records;
5. emit trusted challenge-completion/contribution events;
6. award a small XP transaction and achievement through a separate ledger;
7. display course-specific progress in Course Details and cross-course awards in Profile.

This demonstrates the revised scope without depending on attendance, time online, message counts, or the random activity-tracker placeholder.

## 4. Data boundary recommendation

Do not add gamification arrays directly to `User` or Course models. New collections should reference existing records and carry their own status, version, and audit history. This allows the mock-up to evolve without coupling academic completion rules to reward presentation.

## 5. Current implementation risks to record as requirements

- **Identity spoofing risk:** learner-scoped write routes must not trust a learner ID from the client.
- **Duplicate event risk:** embedded completion objects with timestamps are not naturally idempotent.
- **Mirrored relationship risk:** one action updates multiple models; only one event may award a reward.
- **Course-versus-instance ambiguity:** successful Course completion stores a Course ID, while many features are Course-Instance scoped.
- **Authorization naming risk:** “manager” middleware also allows Teachers; every gamification operation needs an explicit permission decision.
- **Placeholder confusion:** synthetic Activity Tracker data must never be presented as real learner activity.
- **Privacy risk:** social displays must respect the User privacy flag and explicit competition opt-in.
