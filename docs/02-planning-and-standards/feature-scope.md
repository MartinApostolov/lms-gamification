# Revised Gamification Feature Scope

## 1. Scope principle

The feature set is selected according to the main business goals:

1. increase final-exam participation and course completion;
2. maintain motivation throughout and after a course;
3. encourage meaningful cooperation between learners;
4. support Achievers, Socializers, Explorers, and Competitors;
5. avoid encouraging unnecessary website use;
6. keep the implementation focused enough to be completed and integrated reliably.

### 1.1 Outline status

The features below are rough functional outlines. They establish purposes, boundaries, dependencies, and safeguards but do not fix the final interface, terminology, theme, reward amounts, thresholds, or technical implementation.

The scope was revised after stakeholder feedback. See [Stakeholder Feedback and Scope Revision](../01-project-context/stakeholder-feedback-and-scope-revision.md).

## 2. Primary implementation features

### 2.1 Study Groups

#### Purpose

Allow learners in the same course instance to form or join small groups for preparation, mutual support, structured activity, and belonging.

#### Main behavior

- course-instance scope;
- configurable capacity and joining policy;
- voluntary or staff-assigned membership;
- member and organizer roles;
- private group access with staff oversight;
- no reward for joining, remaining, or sending messages;
- direct support for Collaborative Challenges.

#### Main motivation types

Socializers primarily, with support for Achievers and Explorers.

#### Important boundary

Study Groups manages membership and access. It does not itself decide challenge completion, XP, or achievements.

---

### 2.2 Collaborative Challenges

#### Purpose

Give Study Groups, temporary teams, or a course cohort a shared learning or preparation goal based on verified contributions.

#### Main behavior

- visible shared goal, requirements, progress, and availability period;
- trusted learning or task-completion events;
- separate group completion and individual reward eligibility;
- visible minimum individual contribution to prevent free-rider rewards;
- correction and cancellation rules;
- reusable challenge definitions and instances;
- exact activities maintained later in a Challenge Catalogue.

#### Main motivation types

Socializers and Achievers primarily, with support for Competitors and Explorers.

#### Important boundary

A group is an ongoing membership structure. A Collaborative Challenge is a defined activity with eligibility, progress, completion, and reward-source rules.

---

### 2.3 Post-course Knowledge Refreshers

#### Purpose

Help learners retain important knowledge after course completion through short, optional revision activities.

#### Main behavior

- eligibility after trusted course completion;
- configurable delay and optional repeat intervals;
- short quizzes or practical revision activities;
- topic-level feedback;
- links to relevant completed material;
- no penalty for missing or failing an optional refresher;
- limited reward and future Skill Profile integration.

#### Main motivation types

Achievers primarily, with support for Explorers and personal-best Competitors.

#### Important boundary

A refresher does not revoke completed-course status or an existing certificate.

## 3. Supporting mechanics

### 3.1 Course Progress

Shows required progress from 0–100, optional progress from 0–100 where configured, combined points out of 200, and the next meaningful activity.

Required and optional progress remain separate. Optional work does not block normal course completion.

### 3.2 Course Milestones

Recognizes meaningful checkpoints such as Course Started, 25%, Halfway, Required Work Complete, and All Activities Complete.

Milestones use trusted progress or LMS events. They may act as reward sources but are not the main implementation focus.

### 3.3 Final Exam Readiness

Shows the learner's readiness requirements, completed conditions, remaining action, and confirmed exam status where reliable data exists.

Study Group preparation or Collaborative Challenges may appear as optional preparation but must not make personal readiness depend entirely on other learners.

### 3.4 Meaningful XP and Levels

Provides immediate recognition for verified learning, challenge contribution, refresher completion, exam preparation, and course completion.

XP does not replace academic progress, grade, or exam status.

### 3.5 Achievements and Badges

Provides memorable recognition for progress, challenge results, retained knowledge, completion, and optional exploration.

The initial implementation should use only a small catalogue with trusted award sources.

## 4. Later feature variants

### 4.1 Optional Exploration Challenges

Provide voluntary side activities, alternative paths, connected resources, or additional practice.

Optional tasks must not become hidden requirements for normal course completion or final-exam eligibility.

### 4.2 Opt-in Competitive Challenges

Provide personal-best, group, cohort, or team competitions with opt-in participation, privacy controls, fair comparison, tie rules, and periodic resets.

Competition remains a stretch feature after cooperative behavior works reliably.

## 5. Future integration

### 5.1 Skill Profile and Adaptive Learning Paths

The current project may expose skill references and evidence from challenges and refreshers.

A future Skill Profile may support:

- course recommendations;
- prerequisite guidance;
- diagnostic or assessment-first self-paced paths;
- reduced required activities when reliable prior mastery is demonstrated;
- targeted review.

The current project does not implement the skill taxonomy, mastery calculation, recommendation engine, or adaptive completion policy. See [Future Skill Profile Integration](../06-integrations/future-skill-profile-integration.md).

## 6. Removed from active scope

### 6.1 General Course Q&A and Peer Help

This feature is removed because:

- technical questions are likely to be directed to AI assistants or established expert communities;
- remaining posts may often be administrative rather than learning-focused;
- a new LMS Q&A area may remain unused or duplicate stronger external services;
- it creates new moderation, content, and activity models without a clear implementation advantage.

Study Group communication may still exist for coordination within a defined group or Collaborative Challenge.

### 6.2 Reaction-based Peer Contribution Recognition

This feature is removed because:

- learners may not use the reaction mechanism consistently;
- visible or early activity may receive disproportionate attention;
- peer feedback may be biased, ignored, or used negatively;
- reward rules based on reactions may encourage farming or popularity rather than learning.

Individual contribution should instead be verified through the configured activity, challenge rule, assessment, or auditable staff confirmation.

## 7. Other deliberately excluded mechanics

### 7.1 Daily login streaks

These risk encouraging unnecessary website visits and may be unfair to live-course learners whose scheduled activity happens weekly rather than daily.

A meaningful later alternative is post-course revision or learning-continuity activity based on real learning events.

### 7.2 Global public leaderboards

A ranking of all enrolled learners may discourage most participants, create privacy concerns, and produce unfair comparisons.

Small, optional, personal-best, or team-based competition is preferred.

### 7.3 Rewards for time online

Time online does not prove learning and conflicts with the principle that the website should be used only when needed.

### 7.4 Rewards for raw communication volume

Message quantity does not prove useful cooperation and would encourage low-value activity.

## 8. Proposed implementation priority

1. **Required foundation:** trusted events, configuration, audit history, corrections, and duplicate prevention.
2. **Primary MVP:** Study Groups and one complete Collaborative Challenge flow.
3. **Supporting MVP mechanics:** limited XP and achievements connected to the challenge flow, using existing Course Progress or Milestone events where useful.
4. **Recommended extension:** Post-course Knowledge Refreshers.
5. **Later variants:** Optional Exploration Challenges and Opt-in Competitive Challenges.
6. **Future integration only:** Skill Profile and Adaptive Learning Paths.

See [MVP Prioritization](mvp-prioritization.md) for detailed release tiers.

## 9. Data availability warning

The current LMS models reliably expose lesson completion, course completion, program progress, certificates, and live or self-paced course type.

They do not confirm:

- live-session attendance;
- final-exam attendance;
- Study Group membership or communication;
- Collaborative Challenge definitions, contribution, or results;
- refresher schedules, attempts, or topic-level results;
- detailed assessment outcomes;
- Skill Profile data.

Requirements using these events must specify new tracking, integration work, or auditable manual confirmation.
