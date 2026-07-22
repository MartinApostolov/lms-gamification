# Current LMS Map

> **Review basis:** Full supplied LMS mock-up source, not only the original eight model exports. See [Source Note](source-note.md).

## 1. Current system picture

The mock-up is a local LMS with:

1. **Identity and access** — email/password authentication, JWT access control, privacy settings, and the exact roles `GUEST`, `USER`, `TEACHER`, `CONTENT_MANAGER`, and `ADMIN`.
2. **Learning catalogue** — reusable Courses, Seminars, Programs, Categories, and public detail pages.
3. **Learning delivery** — Course Instances and Seminar Instances with schedules, curriculum, staff, enrollment, links, and reminders.
4. **Learning evidence** — tracked course-lesson completion, assessments, quiz and practical exams, results, pass thresholds, practical submissions, successful-course records, program progress, and certificates.
5. **Commercial support** — payments, exam/course enrollment, discount codes, and administrative approval flows.
6. **Content and communication support** — blog, contact forms, files, and reminder infrastructure.

The reusable-template versus concrete-delivery distinction remains central:

- `Course` → reusable definition;
- `CourseInstance` → one live or self-paced delivery;
- `Seminar` → reusable definition;
- `SeminarInstance` → one scheduled delivery.

## 2. Most important current-state corrections

The earlier model-only map understated several available capabilities:

- `Assessment`, `Category`, role constants, controllers, services, routes, and the front end are now available for review.
- Assessment attempts, scores, pass/fail evidence, exam enrollment, exam windows, and practical submissions are implemented.
- Successful Course completion is calculated when a learner has a passing result for **every exam attached to the Course Instance**.
- Certificate issuance is administrator-triggered and also requires every attached exam to be passed.
- Course lesson completion is displayed for instances with `isTracked: true`.

Several previously identified gaps remain:

- no reliable live-session attendance record;
- no seminar completion record;
- no Study Group, Collaborative Challenge, XP, Level, Badge, or Knowledge Refresher model;
- no required-versus-optional lesson classification;
- no general course project/submission workflow separate from practical exams;
- no trusted daily activity or time-spent ledger.

## 3. Important trust warning

The current lesson-completion route should **not yet be used directly as an XP or achievement source**:

- it receives the learner identifier from the URL rather than deriving it from the authenticated token;
- it does not visibly enforce course enrollment in that route;
- its `$addToSet` value includes a fresh timestamp, so repeated calls can create more than one completion object for the same user and lesson.

Course Progress may use the current data for display after deduplicating by learner and lesson, but reward-producing integration requires server-side identity, enrollment, authorization, and idempotency hardening.

## 4. Existing gamification placeholder

The front end exposes `/gamification/activity-tracker`, but the component generates random values in the browser and has no backend source. It is a visual placeholder, not a current activity-tracking capability. It should not influence the functional requirements or be connected to rewards.

## 5. Detailed maps

The full map is split into a subfolder:

- [Detailed map index](current-lms/README.md)
- [Entity relationship map](current-lms/entity-relationship-map.md)
- [Domain and workflow map](current-lms/domain-and-workflow-map.md)
- [Frontend and role map](current-lms/frontend-and-role-map.md)
- [Backend and API map](current-lms/backend-and-api-map.md)
- [Gamification integration assessment](current-lms/gamification-integration-assessment.md)
- [Source evidence index](current-lms/source-evidence-index.md)

## 6. Safe implementation boundary

The gamification subsystem should add separate collections referencing existing LMS records. Existing models can act as source data without receiving XP, badge, group, or challenge fields.

A suitable boundary still includes:

- `GamificationProfile`;
- `GamificationEvent` or trusted source-event ledger;
- `PointTransaction`;
- `AchievementDefinition` and `UserAchievement`;
- `StudyGroup`, membership, and audit records;
- Collaborative Challenge definition, instance, team, contribution, and audit records;
- Knowledge Refresher definition, eligibility, attempt, and result records;
- optional leaderboard snapshots for later opt-in competition.

Adapters should translate existing LMS state changes into idempotent events. Downstream reward features must not watch multiple mirrored arrays independently.
