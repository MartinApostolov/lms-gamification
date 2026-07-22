# Final Consistency Review

## 1. Review scope

This review covers the project overview, revised feature scope, motivation framework, active and supporting feature outlines, the initial badge and XP list, the event matrix, and MVP prioritization.

The documents remain rough functional outlines rather than final product or technical specifications.

The scope revision is recorded in [Stakeholder Feedback and Scope Revision](../01-project-context/stakeholder-feedback-and-scope-revision.md).

## 2. Consistent terminology

The reviewed package uses the following meanings:

- **Learner** is the user participating in a course.
- **Course** is reusable course content.
- **Course instance** is a particular delivery of a course.
- **Required progress** is the 0–100 value used for normal course completion.
- **Optional progress** is a separate 0–100 value for additional learning.
- **Combined progress** is displayed as points out of 200, not as 200% course completion.
- **Course completed** means the configured required course-completion rules are satisfied.
- **All activities complete** means both required and optional work are complete where both exist.
- **Exam Ready** means every active required readiness condition is complete; it does not mean the exam was attended, completed, or passed.
- **Study Group** is an ongoing course-instance membership and access structure.
- **Collaborative Challenge** is a defined shared activity with eligibility, progress, contribution, completion, and correction rules.
- **Group completion** means the shared challenge goal was reached.
- **Individual contribution eligibility** means a learner satisfied the visible personal requirement for a configured reward.
- **Post-course Knowledge Refresher** is a short revision activity offered after trusted course completion.
- **XP** is non-spendable account-wide recognition and does not replace academic progress, grade, exam score, or Skill Profile mastery.
- **Competitors** is used as a neutral design term for the lecture's “Killer” player type.

## 3. Feature boundaries confirmed

- Course Progress calculates required, optional, and combined progress.
- Course Milestones records meaningful checkpoints and publishes a generic milestone event.
- Final Exam Readiness manages exam requirement status and next actions.
- Study Groups manages course-instance group membership, access, roles, and lifecycle.
- Collaborative Challenges manages shared goals, trusted progress, individual contribution, completion, cancellation, and source-result correction.
- Post-course Knowledge Refreshers manages eligibility, revision attempts, topic feedback, and result correction after course completion.
- Meaningful XP and Levels decides XP rules, transactions, limits, and level thresholds.
- Achievements and Badges decides achievement rules, awards, visibility, and revocation.
- Optional Exploration Challenges manages voluntary side activities and optional progress.
- Opt-in Competitive Challenges manages voluntary scoring, ranking, fairness, and privacy.
- Future Skill Profile Integration defines only data and event boundaries; it does not calculate mastery or recommendations.

No source feature fixes an XP amount or badge design. Reward features consume trusted events and apply their own rules.

## 4. Removed feature boundaries

General Course Q&A and reaction-based Peer Contribution Recognition are no longer active feature requirements.

Study Group communication remains possible for coordination within a defined group or challenge, but:

- sending messages does not create XP;
- reactions are not treated as trusted learning evidence;
- the LMS is not required to recreate a general technical Q&A platform;
- administrative questions should use normal course information or support channels.

## 5. Main consistency corrections applied

### 5.1 Implementation focus

Study Groups and Collaborative Challenges are promoted to the primary MVP flow.

Course Progress, Course Milestones, XP, and Achievements remain useful supporting mechanics but are not separate implementation centres for the first demonstration.

### 5.2 Group and individual outcomes

Every Collaborative Challenge separates:

- shared group completion;
- individual contribution eligibility.

This prevents automatic equal personal rewards for inactive members.

### 5.3 Post-course learning

Post-course Knowledge Refreshers are optional revision activities.

Failing or ignoring a refresher does not:

- revoke course completion;
- revoke an existing certificate;
- reduce academic progress;
- create a broken login streak.

### 5.4 Event ownership

Course Milestones publishes `MILESTONE_REACHED` with a milestone type.

Course Progress owns progress-update events. Course completion remains owned by the existing LMS source of truth. Study Groups own membership events. Collaborative Challenges own challenge and contribution events. Knowledge Refreshers own eligibility, attempt, and result events.

XP, Achievements, and future Skill Profile consumers apply their own rules independently.

### 5.5 Correction events

Source features publish correction or revocation events rather than directly deleting downstream XP, achievements, or future skill evidence.

### 5.6 Notifications

Ordinary progress and milestone notifications remain out of scope.

Time-sensitive exam information and newly available refreshers may be notification sources, but delivery, frequency, channels, and user preferences belong to a separate notification mechanism.

### 5.7 Required and optional work

Optional activities, group challenges, and refreshers may provide XP, achievements, optional progress, or review evidence, but they do not silently become normal course-completion requirements.

### 5.8 Skill Profile boundary

Challenges and refreshers may expose skill-tagged evidence in the future.

The current project does not:

- define a skill taxonomy;
- calculate mastery;
- rank course recommendations;
- automatically reduce required content;
- grant course completion from a profile score.

## 6. Remaining decisions deferred to implementation

- exact Study Group creation and joining options implemented in the LMS mock;
- group communication integration and moderation workflow;
- final challenge catalogue and activity ownership;
- trusted contribution source for each challenge type;
- exact XP values, caps, and level thresholds;
- final badge catalogue, names, artwork, and repeatability;
- refresher question formats, timing, pools, and notification limits;
- final-exam eligibility, attendance, completion, and passing data sources;
- event payloads, APIs, queues, and database schemas;
- accessibility, localization, and detailed interface design;
- which staff roles may manually validate or correct each record;
- whether any optional or competitive variant fits the implementation schedule.

## 7. Review conclusion

The revised feature set is internally coherent as a rough product outline.

Its main implementation identity is:

> Study Groups with Collaborative Challenges, supported by meaningful rewards and followed by optional Post-course Knowledge Refreshers.

The main dependencies and source-data gaps are visible, free-rider and reward-farming risks are addressed, and required learning remains separate from optional cooperation, exploration, competition, and post-course revision.

The package is ready for stakeholder confirmation and implementation planning against the supplied LMS mock.
