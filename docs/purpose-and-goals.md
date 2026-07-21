# Purpose and Goals of Gamification

## 1. Background

The LMS has a large difference between initial enrollment and end-of-course participation.

According to the context provided during the lecture, some courses receive approximately 650 enrollments, but only around 15–20% of the enrolled learners attend the final exam. This indicates that the main problem is not attracting learners at the beginning. The larger problem is retaining their participation and motivation throughout the course.

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

## 3. Secondary goal: meaningful learner communication

The system should encourage communication and cooperation between course participants outside scheduled lessons.

Desired behaviors include:

- asking course-related questions;
- providing helpful answers;
- participating in study groups;
- discussing course material;
- sharing useful learning resources;
- preparing for exercises or the final exam together.

The purpose is to create a stronger learning community, reduce isolation, and give learners additional support when they might otherwise stop participating.

## 4. Non-goal: increasing website usage

Increasing time spent on the LMS website is not a success measure by itself.

The system should not reward learners merely for:

- logging in;
- repeatedly opening pages;
- staying online;
- clicking through content;
- sending a large number of low-value messages;
- repeating the same action.

An action should be rewarded only when it represents meaningful progress, preparation, completion, or cooperation.

## 5. Design principles

### 5.1 Reward outcomes and meaningful actions

Suitable reward triggers include:

| Meaningful action | Possible recognition |
|---|---|
| Completing a lesson or required activity | XP or milestone progress |
| Reaching a course checkpoint | Achievement |
| Completing exam-preparation tasks | Challenge progress |
| Attending or completing the final exam | Major achievement |
| Completing the course | Completion badge and XP |
| Making a validated helpful contribution | Contribution recognition |
| Participating in a study-group goal | Collaborative progress |

### 5.2 Avoid rewards that can be farmed

A rule such as “receive XP for every message” would encourage spam. Social rewards should be based on validated usefulness, limited by daily or weekly caps, or connected to a collaborative learning objective.

### 5.3 Keep the final exam visible

Because exam participation is the major drop-off point, the path toward the final exam should be visible throughout the learner journey. Learners should know their current progress, remaining requirements, and preparation status.

### 5.4 Support both live and self-paced learning

The same feature may require different triggers:

- live courses may use scheduled lesson milestones and exam preparation;
- self-paced courses may use lesson completion and flexible progress checkpoints.

The system should not penalize a live-course learner for not visiting the website every day.

### 5.5 Extend, do not modify, the supplied models

Gamification information should be stored in separate models that reference existing users, courses, course instances, and other LMS records.

## 6. Success measures

The main success measures should focus on learning outcomes rather than website traffic.

### 6.1 Final-exam participation rate

```text
Eligible enrolled learners who attend the final exam
-----------------------------------------------------
Total eligible enrolled learners
```

### 6.2 Course completion rate

```text
Learners who successfully complete the course
-----------------------------------------------
Total enrolled learners
```

### 6.3 Retention through course stages

Retention can be measured at significant points, such as:

- after the first lesson;
- at 25% progress;
- at the halfway point;
- shortly before the final exam;
- at final-exam attendance;
- at successful completion.

### 6.4 Meaningful peer participation

Possible indicators include:

- learners who participate in study groups;
- course questions that receive helpful answers;
- learners whose contributions are validated as useful;
- collaborative preparation activities completed by groups.

Raw message count should not be treated as proof of useful communication.

## 7. Summary

The gamification system exists to reduce learner drop-off, increase final-exam participation and course completion, and strengthen meaningful communication between course participants. It must not optimize for unnecessary use of the LMS website.
