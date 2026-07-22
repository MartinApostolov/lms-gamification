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
- Collaborative Challenge requirements;
- Post-course Knowledge Refresher results;
- personal progress statistics.

### Connection to the business goal

Achiever-focused features make the route from enrollment to the final exam visible and manageable. Post-course refreshers also provide evidence that important knowledge has been maintained.

## 3. Socializers

### Main motivation

Socializers are motivated by cooperation, relationships, belonging, and shared goals.

### Suitable LMS features

- Study Groups;
- Collaborative Challenges;
- team exam-preparation goals;
- shared group progress;
- different contribution roles;
- small optional team competitions.

### Safeguards

The system must not reward message quantity, reactions, or group membership by itself.

Possible safeguards include:

- rewards linked to a configured learning objective;
- trusted activity-completion events;
- visible minimum individual contribution;
- staff validation where automatic evidence is unavailable;
- duplicate and correction handling;
- private group access and staff oversight.

## 4. Explorers

### Main motivation

Explorers are motivated by discovery, choice, optional paths, and finding additional knowledge.

### Suitable LMS features

- optional bonus challenges;
- additional learning resources;
- alternative contribution paths;
- discoverable achievements;
- connected-course recommendations;
- optional Post-course Knowledge Refresher review links;
- “extra mile” tasks.

### Safeguards

Exploration must remain optional. Learners should not be required to search through unnecessary website content simply to qualify for course completion.

## 5. Competitors

### Main motivation

Competitors are motivated by comparison, challenge, status, and performing better than others or better than their own previous result.

### Suitable LMS features

- opt-in leaderboards;
- small Study Group or team rankings;
- group competitions;
- time-limited challenges with resets;
- personal-best challenges;
- personal improvement between refresher attempts;
- nearby ranking rather than a full global ranking.

### Safeguards

A public leaderboard across hundreds of learners may discourage people who join late or fall behind. Competitive features should therefore:

- be optional;
- respect user privacy;
- use fair comparison groups;
- avoid public humiliation;
- prefer small groups, teams, or personal-best formats;
- reset periodically where appropriate;
- finalize scores and ties before rewards.

## 6. Feature coverage matrix

| Feature | Achievers | Socializers | Explorers | Competitors |
|---|---:|---:|---:|---:|
| Course Progress | Strong | Low | Strong | Low |
| Course Milestones | Strong | Low | Medium | Low |
| Meaningful XP and Levels | Strong | Medium | Medium | Medium |
| Achievements and Badges | Strong | Medium | Strong | Medium |
| Final Exam Readiness | Strong | Medium | Medium | Low |
| Study Groups | Medium | Strong | Medium | Low |
| Collaborative Challenges | Strong | Strong | Medium | Medium |
| Post-course Knowledge Refreshers | Strong | Low | Medium | Medium |
| Optional Exploration Challenges | Medium | Low | Strong | Low |
| Opt-in Competitive Challenges | Medium | Medium | Low | Strong |

## 7. Example: one preparation period supporting all four motivations

Final Exam Readiness may connect to several preparation paths:

| Component | Motivation supported |
|---|---|
| Complete required preparation milestones | Achievers |
| Complete a Study Group preparation activity | Socializers |
| Explore optional practice material | Explorers |
| Join an optional team or personal-best challenge | Competitors |

## 8. Design rule

The system should offer more than one kind of motivation, but every feature must still support meaningful learning, cooperation, exam participation, course completion, or retained knowledge.
