# Feature Requirements Template

Use this structure for every selected gamification feature.

## Feature name

### 1. What

Describe what the feature is from the learner, lecturer, and administrator perspectives.

### 2. Why

Explain which business or educational problem the feature addresses.

Connect it to one or more goals:

- final-exam participation;
- course completion;
- learner retention;
- meaningful learner cooperation;
- knowledge retention;
- learner motivation.

### 3. How

Define the business behavior:

- trigger events;
- eligibility;
- reward or result;
- frequency and limits;
- duplicate prevention;
- validation;
- revocation or correction;
- configuration;
- visibility;
- privacy.

### 4. Motivation types supported

State how the feature supports:

- Achievers;
- Socializers;
- Explorers;
- Competitors.

A feature does not need to support all four types.

### 5. Live-course behavior

Explain how the feature works for scheduled courses.

Consider:

- scheduled lessons;
- missed or cancelled sessions;
- late enrollment;
- exam preparation;
- attendance data availability.

### 6. Self-paced-course behavior

Explain how the feature works when learners progress at different speeds.

Consider:

- flexible timelines;
- inactivity;
- reopening completed content;
- late completion;
- absence of daily website use.

### 7. Rules and edge cases

Examples:

- Can the reward be earned more than once?
- What happens when an LMS record is corrected?
- Can a learner earn the reward after joining late?
- What happens when a course is cancelled?
- How is spam or reward farming prevented?
- Are private users shown publicly?
- Does a repeated course create a new achievement?

### 8. Acceptance criteria

Write testable statements.

Example:

```text
Given a learner has not previously received the Halfway achievement,
when the learner completes at least 50% of the required course lessons,
then the system awards the achievement once.
```

### 9. Required LMS data

List:

- existing fields or events that can be used;
- missing events or models;
- assumptions requiring confirmation.

### 10. Model extensions

Describe new models that reference the supplied LMS models without changing them.

Possible examples:

- `GamificationProfile`
- `PointTransaction`
- `AchievementDefinition`
- `UserAchievement`
- `Challenge`
- `ChallengeProgress`
- `StudyGroup`
- `CollaborativeChallenge`
- `KnowledgeRefresherDefinition`
- `KnowledgeRefresherAttempt`

### 11. Success measure

Define how the feature's effect will be evaluated.

Examples:

- change in final-exam participation;
- change in course completion;
- percentage of learners reaching milestones;
- percentage participating in useful cooperative activity;
- retained-knowledge performance after course completion.
