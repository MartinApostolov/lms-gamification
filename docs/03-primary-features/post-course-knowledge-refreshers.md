# Post-course Knowledge Refreshers

> **Document status:** This is a rough functional outline. Timing, question formats, reward values, notification behavior, interface details, and technical structures are provisional. See [Document Status and Theming](../02-planning-and-standards/document-status-and-theming.md).

## 1. What

Post-course Knowledge Refreshers help learners retain important knowledge after they have completed a course.

A refresher is a short, optional revision activity that becomes available after a configurable period. It may contain:

- a small quiz;
- a practical question;
- a scenario or code-reading task;
- a short recall exercise;
- a targeted review activity based on important course outcomes.

The learner receives:

- a clear explanation that the activity is post-course revision;
- an estimated completion time;
- results and topic-level feedback;
- links back to relevant lessons or resources;
- an optional meaningful reward for completion or demonstrated retention.

A refresher does not change the historical fact that the learner completed the course.

## 2. Why

Knowledge may weaken after a course ends, particularly when learners do not use it regularly.

The feature provides a meaningful reason to return to the LMS without rewarding empty visits. It can:

- encourage retrieval practice and long-term retention;
- identify topics that need review;
- reconnect learners with previously completed material;
- show related or newly available courses after the learning activity;
- provide future evidence for a Skill Profile;
- support continued learning without requiring daily login streaks.

The return visit is justified by a learning purpose, not by increasing website time as a goal by itself.

## 3. How

### 3.1 Refresher configuration

Authorized course staff should be able to define:

- related course and, where needed, course version;
- title, description, and estimated duration;
- eligible completion event;
- first availability delay after course completion;
- optional repeat intervals;
- question or activity pool;
- topic or skill tags;
- pass, completion, or feedback rules;
- maximum attempts or cooldown where needed;
- reward eligibility;
- enabled status and rule version.

The exact catalogue of refresher content is outside this framework document.

### 3.2 Eligibility

A learner becomes eligible only after a trusted course-completion event or another explicitly configured academic outcome.

Eligibility should record:

- learner;
- course and relevant course instance;
- completion date;
- refresher definition and version;
- eligible-from date;
- expiry date where one exists;
- status.

A duplicated course-completion event must not create duplicated refresher eligibility.

### 3.3 Availability and reminders

A refresher may become available:

- once after a fixed delay;
- at several configured intervals;
- after a previous refresher result indicates that review may be useful;
- when a course owner publishes a new refresher version.

A separate notification mechanism may notify the learner when a refresher becomes available. Notification rules should be limited and configurable.

Missing or ignoring a refresher must not create a penalty, remove XP, break a streak, or reduce completed-course status.

### 3.4 Attempt and result

When a learner starts a refresher, the system should record an attempt.

The result should distinguish:

- completed;
- passed, where a pass rule exists;
- review recommended;
- abandoned;
- invalidated or corrected.

The learner should receive feedback that identifies the relevant topic without unnecessarily exposing answer keys where reuse would be compromised.

### 3.5 Links to review material

Incorrect or uncertain responses may link to:

- the relevant completed lesson;
- a short summary;
- an approved practice resource;
- an optional exploration activity;
- a recommended related course.

The learner should not be forced to repeat the full course because of one weak refresher topic.

### 3.6 Repeat refreshers

Repeated refreshers should use controlled intervals and variation.

The system should avoid:

- showing the same small question set too frequently;
- creating an endless obligation;
- sending excessive reminders;
- awarding repeatable XP without limits;
- treating repeated attempts as new course completion.

A new attempt may be allowed after a configured cooldown or at the next scheduled interval.

### 3.7 Rewards

Possible rewards include:

- limited XP for completing a meaningful refresher;
- a one-time or interval-based achievement;
- a retained-knowledge indicator;
- progress toward a future skill-maintenance record.

Rewards should normally recognize completion or demonstrated retention, not simply opening the refresher page.

Reward rules must define repeatability and duplicate prevention.

## 4. Motivation types supported

- **Achievers — strong:** clear revision targets, results, and evidence of maintained knowledge.
- **Explorers — medium:** optional review links and related learning recommendations.
- **Socializers — low:** the initial refresher is individual, although later group review activities may be added separately.
- **Competitors — low to medium:** a learner may compare against their own previous result; public ranking is not part of this feature.

## 5. Live-course behavior

- Eligibility begins from confirmed course completion, not merely from the scheduled course end date.
- A delayed or rescheduled final exam must not create eligibility until the configured completion source occurs.
- Learners from the same course instance may become eligible at different times.
- Refresher content may reference the version of the live course that the learner completed.

## 6. Self-paced-course behavior

- Eligibility begins from each learner's own completion date.
- Learners may complete refreshers at flexible times within their availability window.
- Inactivity between course completion and the refresher does not create a penalty.
- A future adaptive path may use refresher results as evidence, but this feature does not itself skip required course content.

## 7. Rules and edge cases

- A refresher is optional unless a separate, clearly communicated certification or compliance rule explicitly makes later reassessment mandatory.
- Missing or failing a refresher does not revoke course completion or an existing certificate.
- A course-completion correction may cancel unstarted refresher eligibility.
- A result correction must remain auditable and may reverse an associated reward through the reward feature.
- The same eligibility occurrence must not create duplicate active refreshers.
- Question pools and answer feedback must respect assessment security.
- Refresher data is private to the learner and authorized staff by default.
- Course recommendations shown after a refresher must be clearly separated from the result itself.
- The feature must not use daily login streaks or punish long gaps.
- The learner may review linked content even after the course is completed, subject to normal access rules.

## 8. Acceptance criteria

### AC1 — Create eligibility

Given a learner has a trusted successful course-completion event
and an enabled refresher definition applies,
when the configured delay has passed,
then one eligible refresher record becomes available for that learner and course.

### AC2 — Duplicate completion event

Given refresher eligibility already exists for the same learner, course-completion occurrence, and definition version,
when the completion event is processed again,
then no duplicate eligibility is created.

### AC3 — Start and complete an attempt

Given an eligible refresher is available,
when the learner starts and submits it,
then one attempt and result are stored with the correct learner, course, definition version, and timestamps.

### AC4 — Topic feedback

Given a submitted refresher contains an incorrect or weak response,
when results are shown,
then the learner sees the related topic and at least one approved review link where configured.

### AC5 — No completion revocation

Given a learner fails or ignores an optional refresher,
when course status is evaluated,
then the learner remains course-complete and any existing certificate remains unchanged.

### AC6 — Meaningful reward

Given a refresher reward rule requires completion or a configured result,
when the learner satisfies that rule,
then one reward-source event is generated
and merely opening the refresher creates no reward.

### AC7 — Repeat interval

Given the learner completed a refresher
and another interval is configured,
when the next eligible date arrives,
then a new scheduled occurrence may be created without duplicating the earlier attempt or reward.

### AC8 — Correction

Given an attempt or result was recorded incorrectly,
when authorized staff corrects it,
then the original result remains in the audit history
and downstream reward or skill-evidence consumers can receive a correction event.

### AC9 — Notification independence

Given a refresher becomes available,
when a separate notification feature consumes the eligibility event,
then reminder behavior may be applied without being implemented inside the refresher feature.

## 9. Required LMS data

### Confirmed from the supplied models

- users;
- courses and course instances;
- successful course completion;
- course curriculum and lesson references;
- live or self-paced course type.

### Missing or new data required

- refresher definitions and versions;
- question or activity pools;
- learner eligibility schedules;
- attempts, answers, scores, and topic-level results;
- links between questions, topics, skills, and review material;
- notification preferences and delivery;
- detailed assessment behavior where an existing assessment service is reused;
- final reward rules.

## 10. Model extensions

The supplied LMS models should not be modified.

### `KnowledgeRefresherDefinition`

Stores the course, version, timing, activity pool, topic or skill tags, result rules, reward-source configuration, enabled status, and rule version.

### `LearnerRefresherEligibility`

Stores the learner, related course and course instance, source completion occurrence, definition version, eligible-from date, optional expiry, current status, and deduplication key.

### `KnowledgeRefresherAttempt`

Stores the eligibility record, learner, start and submission times, status, result summary, question or activity version references, and attempt number.

### `KnowledgeRefresherResponse`

Stores the attempt, question or activity reference, learner response, evaluation result, topic or skill references, and feedback metadata where appropriate.

### `KnowledgeRefresherAuditEvent`

Stores corrections, cancellation, rescheduling, manual decisions, and reasons.

## 11. Success measure

Useful indicators include:

- percentage of eligible learners who start and complete a refresher;
- performance by topic and time since course completion;
- percentage of learners who use a linked review resource;
- improvement between refresher attempts;
- return to related learning after a refresher;
- later enrollment in recommended or related courses;
- duplicate, corrected, or invalidated results;
- notification opt-out and reminder fatigue indicators.

Success should be evaluated through retained knowledge and useful follow-up learning, not raw return visits or total website time.

## Related features

- [Meaningful XP and Levels](../04-supporting-mechanics/meaningful-xp-and-levels.md) may recognize valid refresher completion under limited rules.
- [Achievements and Badges](../04-supporting-mechanics/achievements-and-badges.md) may recognize maintained knowledge.
- [Optional Exploration Challenges](../05-later-features/optional-exploration-challenges.md) may provide related optional review activities.
- [Future Skill Profile Integration](../06-integrations/future-skill-profile-integration.md) defines how refresher results may later expose skill evidence.
- [Gamification Event Matrix](../06-integrations/gamification-event-matrix.md) lists proposed refresher events and consumers.
