# Source Evidence Index

This index identifies the principal mock-up paths used by the Current LMS Map. It is not an exhaustive file inventory.

## Project and environment

| Evidence | Source path |
|---|---|
| Local sandbox purpose, startup, roles/accounts, architecture, localization and backend authorization guidance | `README.md` |
| API composition | `lms-be/routes.js`, `lms-be/server.js` |
| Demo data | `lms-be/seeds/contentSeed.js`, `lms-be/seeds/userSeed.js` |

## Roles, identity, and authorization

| Evidence | Source path |
|---|---|
| Exact role values and assessment/content types | `lms-be/constants.js`, `lms-fe/src/constants.js` |
| JWT, owner, administrator, and teacher/content-manager checks | `lms-be/middlewares/auth-middlewares.js` |
| Account and relationship schema | `lms-be/models/User.js` |
| Authentication flow | `lms-be/controllers/auth-controller.js`, `lms-be/services/auth-service.js` |

## Catalogue and delivery

| Evidence | Source path |
|---|---|
| Course template | `lms-be/models/Course.js` |
| Course Instance, tracking, curriculum, lesson completion, exams, enrollment and staff | `lms-be/models/CourseInstance.js` |
| Seminar template and instance | `lms-be/models/Seminar.js`, `lms-be/models/SeminarInstance.js` |
| Program progress/prerequisites | `lms-be/models/Program.js`, `lms-be/controllers/program-controller.js` |
| Course Instance routes | `lms-be/controllers/courseInstance-controller.js` |
| Course Instance business logic | `lms-be/services/courseInstance-service.js` |

## Assessments, exams, completion, and certificates

| Evidence | Source path |
|---|---|
| Assessment types, questions, results, exam windows, enrollment and practical submissions | `lms-be/models/Assessment.js` |
| Assessment/exam access, attempts, results and submissions | `lms-be/services/assessment-service.js` |
| Assessment routes and identity/role checks | `lms-be/controllers/assessment-controller.js` |
| Current all-exams-passed Course completion rule | `lms-be/services/user-service.js` (`updateUserCompletedCourses`) |
| Certificate schema and issuance | `lms-be/models/Certificate.js`, `lms-be/services/certificate-service.js`, `lms-be/controllers/certificate-controller.js` |

## Payments and supporting content

| Evidence | Source path |
|---|---|
| Course/exam payments | `lms-be/models/Payment.js`, `lms-be/controllers/payment-controller.js` |
| Discount targeting | `lms-be/models/DiscountCode.js`, `lms-be/controllers/discount-code-controller.js` |
| Blog | `lms-be/models/BlogPost.js`, `lms-be/controllers/blog-controller.js` |
| Survey, Review, Content, and Session model presence | `lms-be/models/Survey.js`, `Review.js`, `Content.js`, `Session.js` |

## Frontend and integration points

| Evidence | Source path |
|---|---|
| Route/role composition | `lms-fe/src/App.jsx` |
| Learner Course Details | `lms-fe/src/components/Details/Details.jsx` and child components |
| Tracked curriculum behavior | `lms-fe/src/components/Details/DetailsCurriculum/DetailsCurriculum.jsx` |
| Lesson completion UI | `lms-fe/src/components/Details/DetailsCurriculum/DetailsCurriculumLessonContent/DetailsCurriculumLessonContent.jsx` |
| Exam learner UI | `lms-fe/src/components/Details/DetailsQuizSection/DetailsExamSection.jsx`, `lms-fe/src/components/Assessment/` |
| Profile | `lms-fe/src/components/UserProfile/UserProfile.jsx` |
| Teaching and Administration | `lms-fe/src/components/Teaching/Teaching.jsx`, `lms-fe/src/components/Administration/Administration.jsx` |
| Translations | `lms-fe/src/lang/locales/bg_BG.js`, `lms-fe/src/lang/locales/en_US.js` |

## Existing gamification placeholder

| Evidence | Source path |
|---|---|
| Public Activity Tracker route | `lms-fe/src/App.jsx` |
| Random client-only grid | `lms-fe/src/components/ActivityTracker/ActivityTracker.jsx` |
| Minimal rendering test | `lms-fe/src/components/ActivityTracker/ActivityTracker.test.jsx` |
