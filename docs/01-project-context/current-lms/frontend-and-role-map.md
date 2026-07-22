# Frontend and Role Map

## 1. Exact roles

The backend and frontend constants define:

| Role | Main observed purpose |
|---|---|
| `GUEST` | Unauthenticated/public access state |
| `USER` | Learner account |
| `TEACHER` | Teaching, grading, and selected instance-management actions |
| `CONTENT_MANAGER` | Content/instance management and grading |
| `ADMIN` | Full administrative actions, including certificate issuance |

Backend middleware is authoritative. Hiding a frontend control is not sufficient authorization.

`isAdminOrManager` currently allows `ADMIN`, `CONTENT_MANAGER`, and `TEACHER`, despite its shorter name.

## 2. Main learner-facing areas

### Public catalogue and detail pages

- Course and Seminar catalogues;
- Course/Seminar details;
- Program catalogue and Program details;
- enrollment and checkout;
- public certificate display/share;
- blog and general public pages.

### Authenticated learner areas

- Profile with enrollments, payments, and account information;
- course curriculum and tracked lesson completion;
- lesson assessments;
- active exams and exam pages;
- practical-exam upload and own-submission access;
- program progress based on completed Courses.

## 3. Staff areas

### Teaching

The Teaching route is available to Teacher, Content Manager, and Administrator roles and contains schedule/teaching-oriented views.

### Administration

The top-level route is also exposed to Teacher, Content Manager, and Administrator users, while individual backend operations remain role-checked. Administration includes course/seminar, category, schedule, program, payment, discount, user, and blog functionality.

Gamification staff screens must use explicit backend permissions rather than assume that every user who can enter Administration can manage all gamification rules.

## 4. Natural gamification integration points

### Course Details — primary learner integration

Course-instance features should appear within the learner's Course Details experience because that screen already owns:

- enrollment context;
- curriculum and next lesson;
- tracked lesson progress;
- assessments and exams;
- live/self-paced instance details.

Recommended placements:

- Course Progress summary near the curriculum;
- Final Exam Readiness near the exams section;
- Study Group and active Collaborative Challenge cards in the enrolled-only course area;
- a single “Next meaningful action” entry that links directly to the underlying lesson, assessment, group, or challenge.

### Profile — cross-course learner identity

The Profile is the natural location for:

- total XP and level;
- earned achievements/badges;
- privacy and opt-in competitive preferences;
- cross-course history.

Course-specific detailed progress should remain in the Course Instance rather than become an oversized global dashboard.

### Teaching/Administration — staff configuration

Suitable staff functions include:

- create/manage Study Groups;
- assign or configure Collaborative Challenges;
- view group membership and contribution evidence;
- configure progress/readiness requirements;
- audit/reverse reward events;
- maintain achievement and XP rules, subject to role permissions.

## 5. Existing activity-tracker placeholder

`/gamification/activity-tracker` renders a contribution-style grid generated with random values in the browser. It has:

- no authentication requirement on its route;
- no backend storage or API;
- hard-coded English labels instead of the required translation keys;
- a minimal rendering test only.

It should be classified as **Placeholder**. It should either be removed from the functional implementation or rebuilt around meaningful verified events. A GitHub-style daily-activity grid is not recommended for the current business goal because it can encourage unnecessary site visits and imply data that the LMS does not collect.

## 6. Localization and accessibility constraints

New learner and staff text must be added to both Bulgarian and English `react-intl` locale files. Gamification status must not rely on color alone; labels, icons, progress text, and screen-reader descriptions should communicate the state.

## 7. Privacy defaults

The existing User model contains a privacy flag. Personal detailed progress, group membership, contribution history, and exam readiness should be private to the learner and authorized staff by default. Public or cohort comparison requires separate opt-in rules.
