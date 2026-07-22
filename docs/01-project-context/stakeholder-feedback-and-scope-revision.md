# Stakeholder Feedback and Scope Revision

> **Document status:** This document records the current scope decision after lecturer feedback. It explains why the active implementation focus differs from the initial feature list. Exact implementation details may still change after the LMS mock and technical constraints are supplied.

## 1. Feedback received

The initial requirements included a general **Course Q&A and Peer Help** feature and a separate **Peer Contribution Recognition** feature.

During stakeholder review, the following risks were identified:

- learners are likely to direct many technical questions to AI assistants or established specialist communities instead of a new LMS peer forum;
- the remaining LMS questions may often be administrative, such as asking when the next lecture occurs, rather than meaningful learning questions;
- a new general-purpose Q&A area may remain sparsely used and duplicate services that already have a larger expert community;
- learner-driven reactions or review signals may be ignored, inconsistently applied, biased toward visible or early contributions, or used negatively;
- rewarding reactions may shift attention from learning toward collecting feedback signals.

The stakeholder responded more positively to:

- small course-instance Study Groups;
- Collaborative Challenges with shared goals and visible progress;
- optional competitive formats such as group tournaments;
- post-course revision tests that help learners remember material and provide a meaningful reason to return to the LMS;
- future Skill Profiles that could support recommendations and adaptive self-paced course paths.

## 2. Scope decision

The active implementation focus is revised as follows:

1. **Study Groups and Collaborative Challenges become the primary social and cooperative direction.**
2. **Post-course Knowledge Refreshers are added as the recommended learning-retention extension.**
3. **Meaningful XP, Achievements and Badges, Course Progress, and Course Milestones remain supporting mechanics rather than separate implementation centres.**
4. **Optional Exploration Challenges and Opt-in Competitive Challenges remain later variants or stretch features.**
5. **Skill Profile and Adaptive Learning Paths are treated as a future integration contract, not a complete feature in this project.**
6. **Course Q&A and Peer Help is removed from active scope.**
7. **Reaction-based or review-based Peer Contribution Recognition is removed from active scope.**

## 3. Communication boundary

This revision does not remove all learner communication.

Study Groups may still provide or integrate with a private communication space so members can coordinate meaningful course work, prepare for the final exam, and complete Collaborative Challenges. Communication is supporting infrastructure for a defined learning group or activity rather than a new general-purpose Q&A forum.

Administrative questions should be handled through normal course announcements, schedules, help pages, or staff support. Specialist technical questions may be directed to appropriate external communities where suitable.

## 4. Recognition boundary

Learners are not asked to rate one another as the main proof of contribution.

Recognition should come from observable activity within a configured learning objective, for example:

- completing an assigned part of a Collaborative Challenge;
- satisfying a visible minimum individual contribution;
- completing a structured Study Group preparation activity;
- earning a verified challenge result;
- completing a Post-course Knowledge Refresher.

Staff validation may still be used where an automatic source is unavailable, but every manual decision must be auditable.

## 5. Implementation focus

The most important demonstrable flow is:

> An enrolled learner joins or is assigned to a Study Group, contributes to a Collaborative Challenge, sees both group and personal progress, satisfies the minimum personal contribution, and receives a meaningful reward when the group completes the challenge.

The recommended second flow is:

> A learner who completed a course becomes eligible for a short Post-course Knowledge Refresher, receives topic-level feedback, and can return directly to relevant course material.

## 6. Future integration

The current features should remain compatible with a future Skill Profile by allowing:

- challenge definitions to reference skills practised or demonstrated;
- refresher results to produce skill evidence;
- course recommendations to consume skill mastery information;
- future self-paced course rules to reduce or skip already-mastered activities after reliable assessment.

The current project does not define a complete skill taxonomy, recommendation engine, or adaptive course-completion policy.

## 7. Reason for narrowing the scope

The project will be implemented against a supplied LMS mock and later reviewed alongside many other implementations. A smaller, coherent, and reusable module is more likely to be completed well and integrated into a combined system than a broad collection of partially implemented features.
