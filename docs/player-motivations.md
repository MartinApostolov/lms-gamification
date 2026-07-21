# Learner Motivation Types

## 1. Purpose of the framework

The design considers four motivation types discussed in the lecture:

- Achievers
- Socializers
- Explorers
- Killers, referred to in this document as **Competitors**

These types are used as design perspectives, not as permanent labels assigned to users. A learner may respond to several forms of motivation, and their motivation may change during a course.

The purpose of the framework is to check that the gamification system does not depend on only one kind of reward.

## 2. Achievers

### Main motivation

Achievers are motivated by progress, mastery, completion, and visible evidence of accomplishment.

### Suitable LMS features

- course progress indicators;
- milestones;
- meaningful XP and levels;
- completion badges;
- exam-readiness status;
- personal progress statistics;
- course and program completion recognition.

### Connection to the business goal

Achiever-focused features make the route from enrollment to the final exam visible and manageable. They are therefore strongly connected to the main goal of increasing completion.

## 3. Socializers

### Main motivation

Socializers are motivated by communication, cooperation, relationships, and belonging to a learning community.

### Suitable LMS features

- study groups;
- collaborative challenges;
- peer questions and answers;
- recognition for validated helpful contributions;
- team exam-preparation goals;
- shared group progress.

### Safeguards

The system must not reward message quantity by itself. Possible safeguards include:

- helpful marks from other learners;
- lecturer or moderator validation;
- daily or weekly reward limits;
- no rewards for self-reactions;
- no rewards for duplicate or deleted spam;
- rewards linked to a real learning objective.

## 4. Explorers

### Main motivation

Explorers are motivated by discovery, choice, optional paths, and finding additional knowledge.

### Suitable LMS features

- optional bonus challenges;
- additional learning resources;
- alternative preparation activities;
- discoverable achievements;
- connected-course recommendations;
- optional “extra mile” tasks.

### Safeguards

Exploration must remain optional. Learners should not be required to search through unnecessary website content simply to qualify for course completion.

## 5. Competitors

### Main motivation

Competitors are motivated by comparison, challenge, status, and performing better than others or better than their own previous result.

### Suitable LMS features

- opt-in leaderboards;
- small cohort or study-group rankings;
- team competitions;
- weekly challenges with resets;
- personal-best challenges;
- nearby ranking rather than a full global ranking.

### Safeguards

A public leaderboard across hundreds of learners may discourage people who join late or fall behind. Competitive features should therefore:

- be optional;
- respect user privacy;
- use fair comparison groups;
- avoid public humiliation;
- prefer small groups or teams;
- reset periodically where appropriate;
- provide personal-best alternatives.

## 6. Feature coverage matrix

| Feature | Achievers | Socializers | Explorers | Competitors |
|---|---:|---:|---:|---:|
| Course Progress | Strong | Low | Strong | Low |
| Course Milestones | Strong | Low | Medium | Low |
| Meaningful XP and levels | Strong | Low | Medium | Medium |
| Achievements and badges | Strong | Medium | Strong | Medium |
| Final Exam Readiness | Strong | Medium | Medium | Low |
| Course Q&A and peer help | Medium | Strong | Medium | Low |
| Peer contribution recognition | Medium | Strong | Medium | Low |
| Study groups | Medium | Strong | Medium | Low |
| Collaborative challenges | Strong | Strong | Medium | Medium |
| Optional exploration challenges | Medium | Low | Strong | Low |
| Opt-in competitive challenges | Medium | Medium | Low | Strong |

## 7. Example: one challenge supporting all four motivations

Final Exam Readiness can contain several preparation paths:

| Component | Motivation supported |
|---|---|
| Complete required preparation milestones | Achievers |
| Join a group preparation activity | Socializers |
| Explore optional practice material | Explorers |
| Join an optional team or personal-best challenge | Competitors |

## 8. Design rule

The system should offer more than one kind of motivation, but every feature must still support meaningful learning, communication, exam participation, or course completion.
