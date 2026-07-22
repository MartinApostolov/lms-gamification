# Domain and Workflow Map

## 1. Catalogue and delivery domains

### Courses

1. Staff create a reusable `Course` with multilingual descriptions, curriculum, prerequisites, pricing, and catalogue data.
2. Staff create one or more `CourseInstance` records linked to the Course.
3. The instance receives dates, delivery mode, copied curriculum, staff, learners, assessments/exams, links, payments, and reminder settings.
4. A learner enrolls directly or through an approved payment flow.
5. Free exams attached to the instance may be enrolled automatically with the course.

A Course Instance explicitly distinguishes live and non-live delivery through `isLive`.

### Seminars

The Seminar/Seminar Instance structure mirrors the template/delivery split, but Seminar Instances do not contain the course-style lesson `completedBy` tracking and no seminar-completion workflow was found.

### Programs

Programs contain ordered Course templates with prerequisite groups. Progress is calculated from the learner's `successfullyCompletedCourses`, and the model can determine the next available Course and full completion.

## 2. Course learning flow

### Learner view

The Course Details screen provides the strongest existing learner integration point:

- public course information;
- enrollment/payment state;
- enrolled-only curriculum;
- tracked sequential lesson UI for `isTracked` instances;
- lesson assessments;
- exam information and entry;
- practical-exam instructions and submission.

### Tracked lessons

For tracked instances, the frontend filters the lesson completion list to the current learner and identifies the next incomplete lesson. A learner can mark an eligible lesson complete; a passed lesson assessment can also trigger the same completion action in the UI.

This is useful progress evidence, but the backend completion route needs hardening before reward use. See [Backend and API Map](backend-and-api-map.md).

## 3. Assessment and exam flow

`Assessment.assessmentType` supports:

- `ASSESSMENT` — lesson/course assessment;
- `EXAM_QUIZ` — timed or windowed quiz exam;
- `EXAM_PRACTICAL` — practical exam with instructions, submission window, and later grading.

### Assessment evidence

The backend stores attempts/results with scores, pass thresholds, timestamps, counts, and answers. Lesson assessments have a maximum-attempt rule in the application constants.

### Exam access

Exam access can depend on:

- authenticated learner identity;
- presence in `examEnrolledUsers`;
- configured start/end window;
- payment approval for paid exams.

The assessment service centralizes exam-window checks so entry, instruction access, and practical submission use the same decision.

### Practical submission

The learner uploads work during the allowed window. The file is stored outside the publicly served event file tree and can be downloaded only by its owner or a grader role. Re-uploading replaces the previous submission row.

### Grading

Teachers, content managers, and administrators can submit practical results. Quiz results are calculated from answers. Results support pass/fail interpretation by comparing score with the stored pass threshold.

## 4. Successful course completion

The current service marks a Course successfully completed when:

1. it finds the Course Instance containing the assessment that changed;
2. it checks every exam attached to that instance;
3. the learner has a result for every exam;
4. every result score meets that exam's pass score.

The service then adds the Course template to `User.successfullyCompletedCourses` and the learner to `Course.successfullyCompletedByUsers`.

Consequences:

- lesson progress and successful course completion are separate concepts;
- an instance with lessons but no passing exam set does not use lesson completion to create the successful-course record;
- the current completion record is Course-template scoped, not explicitly Course-Instance scoped;
- repeated Course Instances of the same Course require careful interpretation because the durable completion array stores only the Course ID.

## 5. Certificate flow

Certificate issuance is an administrator action.

For each enrolled learner, the service:

- requires a result for every exam;
- requires each result to meet its pass-score snapshot;
- calculates the certificate score as the average of the passed exam scores;
- creates or updates a Certificate;
- references it from User, Course, and Course Instance.

Certificate issuance is therefore a strong server-side achievement event, but it is not automatically identical to the earlier successful-course update and must have its own source identifier.

## 6. Enrollment and payment flow

The mock-up supports free and paid Course/Exam enrollment. Payments reference a User and either a Course Instance or Assessment. Administrative approval can trigger enrollment. Discount Codes can apply to Course Instances, Assessments, or broader configured target types.

Payment completion should not award learning XP. It may only unlock access to learning or exam events.

## 7. Reminder flow

Course and Seminar Instances contain reminder configuration for day-before, day-of, and one-hour-before messages, with timestamps used to avoid repeated sends. The local sandbox disables reminder cron/email by default.

This infrastructure may later carry exam-readiness or refresher notifications, but notification delivery is not itself learning progress.

## 8. Still absent from current workflows

- verified live-class attendance;
- seminar completion;
- Study Groups or group communication;
- Collaborative Challenge definitions, contributions, team progress, or validation;
- XP transactions, levels, badges, or achievement definitions;
- post-course refresher scheduling and topic-level feedback;
- required/optional lesson configuration;
- general activity/time-spent tracking suitable for rewards.
