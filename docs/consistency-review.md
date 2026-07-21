# Final Consistency Review

## 1. Review scope

This review covers the project overview, feature scope, motivation framework, eleven feature outlines, the initial badge and XP list, the event matrix, and MVP prioritization.

The documents remain rough functional outlines rather than final product or technical specifications.

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
- **Accepted solution** is the one answer selected by the asker or authorized staff in Course Q&A and Peer Help.
- **Recognized contribution** is a validated helpful action; raw posts, comments, reactions, and group membership are not recognized contributions by themselves.
- **XP** is non-spendable account-wide recognition and does not replace academic progress, grade, or exam score.
- **Competitors** is used as a neutral design term for the lecture's “Killer” player type.

## 3. Feature boundaries confirmed

- Course Progress calculates required, optional, and combined progress.
- Course Milestones records meaningful checkpoints and publishes a generic milestone event.
- Final Exam Readiness manages exam requirement status and next actions.
- Meaningful XP and Levels decides XP rules, transactions, limits, and level thresholds.
- Achievements and Badges decides achievement rules, awards, visibility, and revocation.
- Course Q&A and Peer Help manages questions, answers, comments, accepted solutions, and moderation.
- Peer Contribution Recognition decides whether a social or collaborative action is sufficiently validated to deserve recognition.
- Study Groups manages membership and access; joining or posting does not award XP by itself.
- Collaborative Challenges manages shared goals and verified individual contribution.
- Optional Exploration Challenges manages voluntary side activities and optional progress.
- Opt-in Competitive Challenges manages voluntary scoring, ranking, fairness, and privacy.

No source feature fixes an XP amount or badge design. Reward features consume trusted events and apply their own rules.

## 4. Main consistency corrections applied

### Event ownership

Course Milestones now publishes `MILESTONE_REACHED` with a milestone type rather than appearing to own every underlying business event.

Course Progress owns progress-update events. Course completion remains owned by the existing LMS source of truth. Exam attendance and completion remain owned by an exam, attendance, or assessment source when one exists.

### Correction events

Challenge documents now describe source-result correction events rather than implying that a challenge feature directly removes XP or badges. XP and Achievements decide how downstream rewards are reversed.

### Notifications

Ordinary progress and milestone notifications remain out of scope. Only time-sensitive exam information is identified as a possible notification source, and delivery belongs to a separate notification mechanism.

### Required and optional work

Optional activities may contribute to optional progress, XP, achievements, and exploration challenges, but they do not block normal course completion or exam eligibility unless a course explicitly defines an underlying activity as required.

### Social rewards

Questions, answers, comments, reactions, messages, group creation, and group membership do not award XP by themselves. Accepted solutions or other validated contributions may create trusted recognition events.

## 5. Remaining decisions deferred to implementation

- exact required and optional activity configuration;
- final-exam eligibility, attendance, completion, and passing data sources;
- exact XP values, caps, and level thresholds;
- final badge catalogue, names, artwork, and repeatability;
- event payloads, APIs, queues, and database schemas;
- moderation staffing and response rules;
- challenge catalogue and content ownership;
- final visual theme and learner-facing terminology;
- accessibility, localization, and detailed interface design;
- which staff roles may manually validate or correct each record.

## 6. Review conclusion

The feature set is internally coherent as a rough product outline. The main dependencies and source-data gaps are visible, reward farming is consistently restricted, and the documents distinguish required learning from optional exploration, social contribution, and opt-in competition.

The package is ready for stakeholder review, technical feasibility assessment, or selection of an MVP implementation scope.
