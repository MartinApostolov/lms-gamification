# Mock-up Requirements Impact Review

> **Document status:** Source-grounding review of the rough functional requirements. It does not finalize names, UI design, thresholds, XP amounts, or database schemas.

## 1. Review purpose

The earlier requirements deliberately recorded many LMS behaviors as assumptions because only a small set of model exports was available. The complete mock-up now provides models, business services, routes, authorization, learner/staff screens, and seed data.

This review records what should be corrected, clarified, or retained.

## 2. Conclusions that remain unchanged

The central product direction remains valid:

- improve retention, final-exam participation, and course completion;
- reward meaningful learning and cooperation rather than clicks, logins, messages, or time online;
- support live and self-paced Course Instances;
- keep competition optional and privacy-aware;
- keep Study Groups separate from Collaborative Challenges;
- distinguish shared challenge completion from individual reward eligibility;
- add gamification through separate models and trusted events.

## 3. New confirmed LMS facts

The mock-up confirms:

- exact roles and backend authorization middleware;
- tracked course lessons with learner completion timestamps;
- `isLive` and `isTracked` Course Instance flags;
- assessments, quiz exams, practical exams, results, scores, pass thresholds, and answers;
- exam enrollment, date/time windows, duration, price, instructions, and practical submissions;
- successful Course completion after all Course Instance exams are passed;
- administrator-issued Certificates with averaged exam score;
- Program progress/completion based on completed Course templates;
- Profile, Course Details, Teaching, and Administration integration points.

## 4. Corrections to earlier assumptions

### Assessment outcomes

Assessment outcomes are not missing. They are stored in `Assessment.results`, including score, pass-score snapshot, timestamps, question counts, answer counts, and given answers.

### Exam completion and practical work

The LMS can record a quiz result and a practical submission/result. It still does not record a separate “exam attended” event, so attendance must not be inferred from enrollment, submission, or the date passing.

### Course completion

The current completion rule is not “all required lessons completed.” The service records successful Course completion when all exams attached to the Course Instance have passing results. Course Progress must therefore remain separate from the existing academic completion source of truth.

### Roles and UI

Roles and UI are available. Requirements should name learner, teacher, content manager, and administrator behaviors while still allowing permission details to be refined.

## 5. Feature impacts

### 5.1 Course Progress

Retain the required/optional/combined concept, but ground the first version in `CourseInstance.isTracked` and lesson `completedBy` data.

Required changes:

- define whether a tracked lesson is required or optional because the current schema does not;
- deduplicate completion by learner and lesson;
- secure the backend completion operation before rewards consume it;
- state clearly that required progress does not itself create the existing successful-Course record;
- use the current Course Details curriculum as the first learner UI location.

### 5.2 Course Milestones

Initial milestones may use:

- first trusted lesson completion;
- 25%, 50%, 75%, and 100% de-duplicated required progress;
- all required readiness conditions completed;
- all Course Instance exams passed / Course completion recorded;
- Certificate issued;
- Program milestones.

Do not create milestones for enrollment, payment, opening pages, or random daily activity.

### 5.3 Final Exam Readiness

This feature now has strong source data for:

- exam existence and type;
- enrollment;
- start/end window;
- instruction file;
- quiz result;
- practical submission;
- practical result;
- pass/fail status.

It still needs its own configurable checklist and learner status. “Exam Attended” remains unavailable unless a new attendance source is added.

### 5.4 Study Groups

No current group or messaging subsystem exists. The feature remains new.

Grounded integration decisions:

- scope each initial group to a Course Instance and require LMS enrollment;
- expose learner actions inside enrolled Course Details;
- expose group configuration/oversight in Teaching or Administration;
- enforce membership and staff access on the backend;
- use a dedicated communication area or explicit external integration rather than assume one exists;
- never award XP for creating, joining, remaining in, or messaging a group.

### 5.5 Collaborative Challenges

No current challenge framework exists. The feature remains new.

Existing LMS evidence can contribute to selected challenge requirements after adaptation:

- trusted assessment completion/pass;
- practical submission occurrence;
- Course Progress milestones;
- existing Course/Program completion.

Lesson-completion events must not be used as reward-capable challenge contributions until hardened. Challenge-specific deliverables and peer/staff validation require new records.

### 5.6 Meaningful XP and Levels

No XP/level model exists. Add a transaction ledger rather than a mutable total-only field.

Strong initial sources:

- all attached exams passed / Course completion recorded;
- Certificate issued;
- Program milestone/completion;
- verified Collaborative Challenge contribution and completion;
- completed post-course refresher.

Potential source after hardening:

- unique required lesson completion or progress milestone.

Excluded sources:

- payment;
- enrollment alone;
- login;
- page view;
- time online;
- message count;
- random Activity Tracker cell.

### 5.7 Achievements and Badges

Course completion, Certificate issuance, Program completion, verified challenge contribution, and future refresher completion are technically meaningful sources. Score-based achievements are possible, but thresholds must be course-aware and should not encourage repeated low-value attempts.

### 5.8 Post-course Knowledge Refreshers

The current Assessment engine provides useful concepts—questions, answers, attempts, scores, timestamps—but a Refresher is not currently implemented.

A Refresher still needs:

- eligibility after trusted Course completion;
- delayed scheduling and expiration;
- definition/rule version;
- topic mapping;
- topic-level feedback;
- links back to completed material;
- separation from official Course completion and Certificate records.

### 5.9 Optional and competitive challenges

No existing framework changes the “later” classification. Competitive views require explicit opt-in and must respect User privacy.

## 6. Existing Activity Tracker decision

The current Activity Tracker must not be treated as an implemented gamification feature. Its values are random, client-only, unauthenticated, and unconnected to learning data. It conflicts with the requirement to avoid rewarding unnecessary site activity.

Recommended disposition:

- remove or hide it for the functional MVP; or
- rebuild it later as a meaningful-event history, using real labels such as lesson completed, assessment passed, challenge contribution verified, or refresher completed.

A calendar grid should not be the main learner goal because meaningful learning may happen in irregular sessions, especially for live courses.

## 7. Revised implementation priority

### Tier 0 — integration safety

- secure and deduplicate lesson completion;
- establish authoritative event IDs and correction behavior;
- define Course-versus-Course-Instance scope;
- define explicit gamification permissions.

### Tier 1 — demonstration path

- Course Progress in one tracked Course Instance;
- Study Group membership;
- one Collaborative Challenge;
- verified individual contribution;
- XP ledger and one achievement;
- Course Details/Profile display.

### Tier 2 — exam journey

- Final Exam Readiness using real exam/enrollment/window/result data;
- milestone and notification integration;
- Certificate event integration.

### Tier 3 — extension

- Post-course Knowledge Refreshers;
- broader achievement catalogue;
- later exploration and opt-in competition.

## 8. Open decisions after source review

- Which current lessons count as required, optional, or excluded?
- Should Course Progress be enabled only when `isTracked` is true?
- How should completion be represented when the same Course has multiple Course Instances?
- Which roles may create learner groups, assign groups, validate contributions, change rules, and reverse rewards?
- Is group communication built into the LMS or linked to an approved external tool?
- Which exam conditions are eligibility requirements versus informational preparation steps?
- How are corrected/deleted assessment results and revoked Course completions represented?
- Should the existing Activity Tracker be removed, replaced, or retained only as a visual prototype outside the main flow?
