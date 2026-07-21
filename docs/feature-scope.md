# Initial Gamification Feature Scope

## 1. Scope principle

Features are selected according to the main business goals:

1. increase final-exam participation and course completion;
2. maintain motivation throughout the course;
3. encourage meaningful communication between learners;
4. support Achievers, Socializers, Explorers, and Competitors;
5. avoid encouraging unnecessary website use.

### 1.1 Outline status

The features below are rough functional outlines. They establish purposes, boundaries, dependencies, and safeguards but do not fix the final interface, terminology, theme, reward amounts, thresholds, or technical implementation.

A later visual direction may present the same mechanics through a conventional LMS interface or a stronger theme, such as courses as campaign maps, study groups as adventuring parties, and challenges as quests. See [Document Status and Theming](document-status-and-theming.md).

## 2. Core features

### 2.1 Course Progress

#### Purpose

Show required progress from 0–100, optional progress from 0–100, combined progress out of 200 points, and the next meaningful activity.

#### Main motivation types

Achievers and Explorers primarily.

#### Important note

Required and optional progress are separate. Optional work does not block normal course completion.

---

### 2.2 Course Milestones

#### Purpose

Recognize meaningful checkpoints such as Course Started, 25%, Halfway, Required Work Complete, and All Activities Complete.

#### Main motivation types

Achievers primarily, with some support for Explorers.

#### Important note

Milestones use progress or confirmed LMS events. Ordinary milestone notifications are not required.

---

### 2.3 Meaningful XP and Levels

#### Purpose

Provide immediate recognition for real learning progress.

#### Possible XP triggers

- completing a lesson or required activity;
- reaching a course milestone;
- completing exam-preparation requirements;
- attending or completing the final exam;
- completing a course or program;
- making a validated helpful contribution.

#### Actions that should not award XP

- logging in;
- opening a page;
- staying online;
- repeatedly performing the same action;
- sending unvalidated messages.

#### Main motivation types

Achievers primarily, with secondary support for Explorers and Competitors.

---

### 2.4 Achievements and Badges

#### Purpose

Recognize meaningful accomplishments in a visible and memorable way through configurable achievement rules and learner-facing badges.

#### Main behavior

- use reliable LMS or gamification events;
- support global, course, course-instance, program, and explicitly repeatable scopes;
- prevent duplicate awards;
- allow validated manual awards where automatic data is unavailable;
- keep detailed achievement history private by default;
- preserve an audit history for corrections and revocations.

#### Main motivation types

Achievers and Explorers, with secondary support for Socializers and Competitors.

#### Important note

A small initial list of working badges and XP sources is available in [Initial Badges and XP Sources](badges-and-xp-sources.md). Exact earning conditions, values, artwork, and the final catalogue remain deferred until implementation.

---

### 2.5 Final Exam Readiness

#### Purpose

Directly address the major drop-off between enrollment and final-exam participation.

#### Possible tasks

- complete required lessons;
- complete required assignments or assessments, where data is available;
- review final-exam information;
- complete a practice activity;
- join an optional preparation discussion or study group;
- confirm intention to attend;
- reach the course-specific eligibility requirements.

#### Reward

Possible rewards include XP, an exam-related achievement, visible readiness status, or progress toward a larger course-completion achievement.

#### Main motivation types

Can support all four motivation types through personal, social, exploratory, and optional competitive activities.

#### Dependency

The supplied models do not confirm final-exam attendance or all assessment outcomes. These events may require additional tracking.

---

### 2.6 Course Q&A and Peer Help

#### Purpose

Give each course instance a structured place for learners to ask questions, provide answers, discuss clarification in comments, and mark one answer as the accepted solution.

#### Main behavior

- course-instance access for enrolled learners and authorized staff;
- separate questions, answers, and comments;
- one accepted solution per question;
- asker or authorized staff may accept, change, close, or reopen;
- moderation, duplicate handling, and correction events;
- no XP for posting alone.

#### Main motivation types

Socializers primarily, with secondary support for Achievers and Explorers.

#### Dependency

The supplied models do not include discussions, posts, answers, comments, or moderation. New communication models or an integration are required.

---

### 2.7 Peer Contribution Recognition

#### Purpose

Recognize useful learner-to-learner support after it has been validated.

#### Possible recognized actions

- an answer accepted as the solution to another learner's question;
- a useful course resource approved by staff;
- a verified explanation or review contribution in a study group;
- meaningful individual work in a collaborative challenge.

#### Anti-abuse rules

- no XP for every message;
- no self-validation or reward-validating self-answers;
- one active recognition per source occurrence;
- configurable limits or diminishing XP;
- duplicate, plagiarism, spam, and collusion review;
- revoked rewards when validated content is removed.

#### Main motivation types

Socializers primarily, with secondary support for Achievers and Explorers.

---

### 2.8 Study Groups

#### Purpose

Allow learners in the same course instance to form or join small groups for discussion, mutual support, practice, and final-exam preparation.

#### Main behavior

- voluntary, requested, invited, or staff-assigned membership;
- configurable capacity and group roles;
- private group access with staff oversight;
- no rewards for joining, remaining, or posting by itself;
- may later be used by collaborative challenges.

#### Main motivation types

Socializers primarily, with support for Achievers and Explorers.

#### Dependency

Study-group membership, communication, moderation, and audit data require new models or integrations.

---

### 2.9 Collaborative Challenges

#### Purpose

Give study groups, temporary teams, or course cohorts a shared learning or preparation goal based on verified contributions.

#### Main behavior

- visible team goal, requirements, progress, and period;
- trusted learning or contribution events;
- separate team completion and individual reward eligibility;
- minimum individual contribution to prevent free-rider rewards;
- correction and cancellation rules;
- exact challenges maintained later in a Challenge Catalogue.

#### Main motivation types

Socializers and Achievers primarily, with support for Competitors and Explorers.

---

### 2.10 Optional Exploration Challenges

#### Purpose

Provide discovery and choice without making optional website activity mandatory.

#### Possible activities

- optional practice material;
- connected learning resources;
- alternative solution paths;
- bonus course-related challenges;
- hidden or discoverable achievements.

#### Main motivation types

Explorers primarily.

#### Safeguard

Optional tasks must not become hidden requirements for final-exam eligibility or normal course completion.

---

### 2.11 Opt-in Competitive Challenges

#### Purpose

Provide friendly competition for learners motivated by comparison.

#### Possible formats

- personal-best challenges;
- team competitions;
- study-group leaderboards;
- weekly or milestone-based rankings;
- nearby ranking among similar learners.

#### Main motivation types

Competitors primarily.

#### Safeguards

- opt-in participation;
- privacy controls;
- fair comparison groups;
- periodic resets;
- no public display of inactive or low-ranked learners;
- no permanent disadvantage for late enrollment.

## 3. Features not prioritized for the first version

### 3.1 Daily login streaks

These risk encouraging unnecessary website visits and may be unfair to live-course learners whose scheduled activity happens weekly rather than daily.

A possible later alternative is a meaningful learning-continuity measure based on course activity instead of logins.

### 3.2 Global public leaderboards

A ranking of all enrolled learners may discourage most participants, create privacy concerns, and produce unfair comparisons.

Small, optional, or team-based competition is preferred.

### 3.3 Rewards for time online

Time online does not prove learning and conflicts with the project principle that the website should be used only when needed.

### 3.4 Rewards for raw message count

This would encourage spam and low-quality communication.

## 4. Proposed implementation priority

The feature set is divided into four release tiers:

1. **Essential MVP:** Course Progress, Course Milestones, limited Final Exam Readiness, basic Meaningful XP and Levels, and a small Achievements and Badges set.
2. **Recommended after MVP:** Course Q&A and Peer Help together with Peer Contribution Recognition.
3. **Later expansion:** Study Groups, Collaborative Challenges, and Optional Exploration Challenges.
4. **Optional later feature:** Opt-in Competitive Challenges.

All reward-capable features depend on a trusted event, audit, correction, and duplicate-prevention foundation. See [MVP Prioritization](mvp-prioritization.md) for the rationale and suggested sequence.

## 5. Data availability warning

The current LMS models reliably expose lesson completion, course completion, program progress, certificates, and live/self-paced course type.

They do not confirm:

- live-session attendance;
- final-exam attendance;
- discussion messages;
- helpful reactions;
- study groups;
- seminar completion;
- detailed assessment outcomes.

Requirements using these events must specify new tracking or integration work.
