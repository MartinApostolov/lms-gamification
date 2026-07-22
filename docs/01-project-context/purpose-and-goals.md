# Purpose and Goals of Gamification

## 1. Background

The LMS has a large difference between initial enrollment and end-of-course participation.

According to the context provided during the lecture, some courses receive approximately 650 enrollments, but only around 15–20% of the enrolled learners attend the final exam. This indicates that the main problem is not attracting learners at the beginning. The larger problem is retaining participation and motivation throughout the course.

The courses are not delivered mainly through the LMS website. Unlike platforms where the complete learning experience consists of watching videos and completing activities on the website, much of the learning may happen during live lessons or outside the platform.

The gamification system must therefore avoid treating website activity as a goal by itself.

## 2. Primary business goal

The primary goal is to increase the percentage of enrolled learners who remain engaged until the end of the course, attend the final exam, and successfully complete the course.

Gamification should help learners:

- understand where they are in the course;
- see achievable intermediate milestones;
- maintain motivation between lessons;
- recover after falling behind;
- prepare for the final exam;
- understand what remains before completion;
- feel that completing the course is realistic and worthwhile.

## 3. Secondary goal: meaningful learner cooperation

The system should encourage cooperation between course participants outside scheduled lessons without creating activity merely for activity's sake.

Desired behaviors include:

- participating in Study Groups with a defined learning purpose;
- completing Collaborative Challenges;
- preparing for exercises or the final exam together;
- completing assigned parts of a shared task;
- sharing approved learning resources within a group activity;
- supporting group members through structured review or practice.

The purpose is to create belonging, reduce isolation, and give learners additional support when they might otherwise stop participating.

A general Course Q&A platform and reaction-based peer review are not active implementation goals after stakeholder feedback. See [Stakeholder Feedback and Scope Revision](stakeholder-feedback-and-scope-revision.md).

## 4. Long-term learning goal

The system should also support retention after course completion.

Post-course Knowledge Refreshers may:

- prompt short retrieval practice after a configurable period;
- identify topics that need review;
- link learners back to relevant completed material;
- provide a meaningful reason to return to the LMS;
- expose future evidence for a Skill Profile;
- show related courses after the revision activity.

The goal is retained knowledge, not return visits by themselves.

## 5. Non-goal: increasing website usage

Increasing time spent on the LMS website is not a success measure by itself.

The system should not reward learners merely for:

- logging in;
- repeatedly opening pages;
- staying online;
- clicking through content;
- sending a large number of low-value messages;
- joining a group without participating in a learning objective;
- repeating the same action.

An action should be rewarded only when it represents meaningful progress, preparation, completion, cooperation, or knowledge retention.

## 6. Design principles

### 6.1 Reward outcomes and meaningful actions

| Meaningful action | Possible recognition |
|---|---|
| Completing a lesson or required activity | XP or milestone progress |
| Reaching a course checkpoint | Achievement |
| Completing exam-preparation tasks | Readiness or challenge progress |
| Attending or completing the final exam | Major achievement |
| Completing the course | Completion badge and XP |
| Completing a verified part of a Collaborative Challenge | Individual contribution and XP |
| Completing a Study Group goal | Group progress |
| Completing a Post-course Knowledge Refresher | Limited XP, achievement, or retention evidence |

### 6.2 Avoid rewards that can be farmed

Rules must not reward raw messages, reactions, repeated page actions, or membership alone.

Collaborative rewards should be based on:

- verified activity completion;
- visible contribution requirements;
- trusted assessment or LMS events;
- auditable staff confirmation where automation is unavailable;
- duplicate prevention and correction.

### 6.3 Keep the final exam visible

Because exam participation is the major drop-off point, the path toward the final exam should be visible throughout the learner journey. Learners should know their current progress, remaining requirements, and preparation status.

### 6.4 Support both live and self-paced learning

The same feature may require different triggers:

- live courses may use scheduled lesson blocks, Study Groups, and exam-preparation periods;
- self-paced courses may use lesson completion, flexible progress stages, asynchronous groups, and learner-specific refresher dates.

The system should not penalize a live-course learner for not visiting the website every day.

### 6.5 Keep group completion and individual contribution separate

A group may complete a Collaborative Challenge while one member has not completed the visible minimum personal contribution.

The system should record:

- whether the group completed the shared goal;
- whether each learner qualifies for a personal reward.

Membership alone is not proof of contribution.

### 6.6 Extend, do not modify, the supplied models

Gamification information should be stored in separate models that reference existing users, courses, course instances, and other LMS records.

### 6.7 Preserve future integration

Challenges and refreshers may expose skill-related evidence in the future, but the current project does not implement a complete Skill Profile or adaptive course engine.

## 7. Success measures

The main success measures should focus on learning outcomes rather than website traffic.

### 7.1 Final-exam participation rate

```text
Eligible enrolled learners who attend the final exam
-----------------------------------------------------
Total eligible enrolled learners
```

### 7.2 Course completion rate

```text
Learners who successfully complete the course
-----------------------------------------------
Total enrolled learners
```

### 7.3 Retention through course stages

Retention can be measured at significant points, such as:

- after the first lesson;
- at 25% progress;
- at the halfway point;
- shortly before the final exam;
- at final-exam attendance;
- at successful completion.

### 7.4 Meaningful cooperative participation

Possible indicators include:

- learners who participate in active Study Groups;
- Collaborative Challenge participation and completion;
- percentage of members meeting the minimum individual contribution;
- distribution of work across group members;
- movement from group activity to later course milestones and exam readiness;
- learner feedback on usefulness, fairness, and belonging.

Raw message count and group membership alone are not proof of useful cooperation.

### 7.5 Knowledge retention

Possible indicators include:

- eligible learners who complete a refresher;
- topic performance by time since course completion;
- improvement between refresher attempts;
- use of linked review material;
- continued learning or related-course enrollment after a refresher.

Raw return visits are not a knowledge-retention measure.

## 8. Summary

The gamification system exists to reduce learner drop-off, increase final-exam participation and course completion, strengthen meaningful cooperation through Study Groups and Collaborative Challenges, and support knowledge retention after completion. It must not optimize for unnecessary use of the LMS website.
