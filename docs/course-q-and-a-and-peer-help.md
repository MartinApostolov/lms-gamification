# Course Q&A and Peer Help

> **Document status:** This is a rough functional outline. Names, thresholds, rewards, interface details, and technical structures are provisional. See [Document Status and Theming](document-status-and-theming.md).

## 1. What

Course Q&A and Peer Help gives each course delivery a structured posts section where enrolled learners can ask course-related questions and receive answers from peers or authorized staff.

The feature is tied primarily to a **course instance**, so learners ask the people studying the same delivery of the course.

A question post should support:

- a title and question body;
- optional reference to a lesson or course activity;
- answers;
- comments used for clarification;
- one accepted solution;
- open, solved, closed, and moderated states;
- filtering or searching by status and course context.

The learner who asked the question, or an authorized lecturer, moderator, or administrator, may mark one answer as the accepted solution. Marking a solution normally changes the question to **Solved** and closes it to new answers. Authorized staff or the question author may reopen it when the solution is no longer sufficient.

This feature creates trusted discussion events. It does not directly define XP values or achievements. Peer Contribution Recognition, Meaningful XP and Levels, and Achievements and Badges may use an accepted-solution event.

## 2. Why

Learners may stop participating when they become stuck between lessons or feel isolated. A course-specific Q&A area gives them a clear place to ask for help and allows peers to support one another.

The feature supports:

- meaningful communication outside scheduled lessons;
- faster resolution of learning problems;
- reuse of helpful answers for other learners in the same course instance;
- recognition of genuinely useful peer contributions;
- stronger connection between learners preparing for the final exam.

It must not become a source of points for posting volume. Questions, answers, and comments receive no reward merely for existing.

## 3. How

### 3.1 Course scope and access

By default, a Q&A section belongs to one course instance.

The following users may access it:

- learners enrolled in that course instance;
- assigned lecturers and course managers;
- authorized moderators and administrators.

Learners who are not members of the course instance should not see its posts unless a later sharing policy explicitly allows it.

### 3.2 Questions, answers, and comments

A **question** starts a help request. An **answer** proposes a solution. A **comment** asks for clarification or discusses a specific question or answer.

Only answers may be marked as the accepted solution. Comments do not qualify as solutions and do not create accepted-solution rewards.

The system should display the author and timestamps and should preserve an edit history for content that has already received answers, moderation action, or contribution recognition.

### 3.3 Accepted solution

A question may have no more than one active accepted solution.

The following may mark or change the accepted solution:

- the learner who created the question;
- an assigned lecturer or course manager;
- an authorized moderator or administrator.

A learner cannot earn an accepted-solution reward by answering their own question. Marking one’s own answer as the solution must be blocked.

When an eligible answer is accepted, the system should generate a trusted `ANSWER_ACCEPTED` event containing the question, answer, asker, answerer, course instance, validator, and time.

Changing or removing the accepted solution should generate a correction event so that downstream recognition and XP can be reviewed or reversed.

### 3.4 Closing and reopening

Marking an answer as accepted normally changes the question to **Solved** and closes it to new answers.

A question may also be closed without a solution by authorized staff, for example when it is a duplicate, off-topic, no longer relevant, or violates course rules.

The question author or authorized staff may reopen a solved question when more help is required. Reopening does not automatically remove the accepted solution unless the solution is explicitly unmarked.

### 3.5 Moderation

Authorized staff should be able to:

- edit or remove inappropriate content;
- close, reopen, or lock questions;
- mark duplicates and link to the existing question;
- change or remove an accepted solution;
- record a moderation reason;
- view reports and audit history.

Removed or moderated content must not remain an active source of rewards. Corrections should be sent to downstream recognition systems.

### 3.6 Reward integration

Creating a question, answer, or comment does not directly award XP.

Possible trusted events include:

- `QUESTION_CREATED` for analytics only;
- `ANSWER_CREATED` for activity history only;
- `ANSWER_ACCEPTED` for validated contribution recognition;
- `ANSWER_UNACCEPTED` or `CONTENT_REMOVED` for correction;
- `QUESTION_SOLVED` for course-support analytics.

The accepted-solution event may later award XP or an achievement according to separate rules and limits.

## 4. Motivation types supported

- **Socializers — strong:** structured peer communication and mutual support.
- **Achievers — medium:** solving questions can receive validated recognition.
- **Explorers — medium:** learners may discover explanations and alternative approaches.
- **Competitors — low:** public comparison is not part of the Q&A feature.

## 5. Live-course behavior

- Learners may ask questions between scheduled lessons.
- Posts may reference a scheduled lesson, but the lesson date passing does not close the discussion.
- Late-enrolling learners may read existing accessible questions and ask new ones.
- Cancelled or rescheduled lessons should keep associated posts but display updated lesson context where available.
- Lecturers may pin exam-preparation or frequently asked questions.

## 6. Self-paced-course behavior

- Learners may ask questions at different stages of the course.
- The interface should show the referenced lesson or activity to reduce confusion between learners at different points.
- Taking a break does not remove access to existing questions while enrollment remains valid.
- Old solved questions remain searchable unless archived by policy.

## 7. Rules and edge cases

- A learner cannot mark their own answer as the accepted solution to their own question.
- One question can have only one active accepted solution.
- An accepted solution may be changed when a better or corrected answer is provided.
- Duplicate questions may be closed and linked to the original.
- Deleted, abusive, plagiarized, or incorrect answers are not valid reward sources.
- Editing an accepted answer does not create another reward event; significant edits remain auditable.
- Closing a question without a solution creates no accepted-solution reward.
- Course completion and final-exam eligibility do not depend on posting in Q&A unless a separate explicit course requirement exists.
- Anonymous posting is not included in the first version because validation and moderation require reliable authorship.
- Notifications for new answers are outside the current feature scope.

## 8. Acceptance criteria

### AC1 — Create a question

Given a learner is enrolled in a course instance,
when they submit a valid course-related question,
then the question is visible to authorized participants of that course instance with an Open status.

### AC2 — Add an answer

Given a question is open,
when another authorized course participant submits an answer,
then the answer is attached to the question with its author and creation time
and no XP is awarded merely for posting it.

### AC3 — Accept a solution

Given an eligible answer was written by another learner,
when the question author or authorized staff marks it as the accepted solution,
then it becomes the only active accepted solution,
the question becomes Solved,
and one `ANSWER_ACCEPTED` event is generated.

### AC4 — Self-answer restriction

Given a learner created both the question and an answer,
when they attempt to mark their own answer as the accepted solution,
then the system rejects the action as a reward-validating solution.

### AC5 — Change solution

Given a question already has an accepted solution,
when an authorized user accepts a different answer,
then the earlier solution is unmarked,
the new solution is accepted,
and correction and validation events are generated without duplicate active rewards.

### AC6 — Close without solution

Given a question is off-topic, duplicated, or no longer relevant,
when authorized staff closes it without accepting an answer,
then the question is closed
and no accepted-solution event is generated.

### AC7 — Remove rewarded answer

Given an accepted answer is removed for a valid moderation reason,
when the removal is confirmed,
then it is no longer the active solution
and downstream recognition systems receive a correction event.

### AC8 — Course privacy

Given a learner is not enrolled in the course instance and has no authorized staff role,
when they attempt to view its Q&A posts,
then access is denied.

## 9. Required LMS data

### Confirmed from the supplied models

- users;
- courses and course instances;
- learner enrollment and staff relationships where available;
- lessons that may be referenced by a post.

### New data required

- questions, answers, and comments;
- post status and accepted-solution state;
- edit and moderation history;
- course-instance access rules;
- report and content-removal records;
- reliable events for contribution recognition and corrections.

## 10. Model extensions

The supplied LMS models should not be modified.

### `CourseQuestion`

Stores the course instance, author, title, body, optional lesson reference, status, accepted answer, timestamps, and closing or moderation information.

### `CourseAnswer`

Stores the question, author, answer body, edit status, moderation status, and timestamps.

### `CourseComment`

Stores a comment attached to a question or answer, its author, body, moderation status, and timestamps.

### `DiscussionAuditEvent`

Stores accepted-solution changes, status changes, edits requiring history, moderation actions, actor, reason, and time.

## 11. Success measure

Useful indicators include:

- percentage of course questions receiving at least one answer;
- percentage receiving an accepted solution;
- median time from question creation to accepted solution;
- number and proportion of learners who ask or answer at least one course-related question;
- repeat participation after receiving help;
- movement of helped learners toward later progress and exam-readiness stages;
- moderation, duplicate, and reward-reversal rates.

Raw post or comment volume is not a success measure by itself.

See [Gamification Event Matrix](gamification-event-matrix.md) for proposed event ownership and integrations.
