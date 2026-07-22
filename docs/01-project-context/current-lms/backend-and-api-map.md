# Backend and API Map

## 1. Architecture

- Node.js and Express API;
- Mongoose models backed by local MongoDB in the sandbox;
- controllers define route handlers;
- services contain most business logic;
- JWT authentication middleware attaches the verified user to the request;
- selected multi-document actions use MongoDB transactions;
- the router is mounted both at the root and `/api` in the local training environment.

## 2. Main route families

| Route family | Main responsibility |
|---|---|
| `/auth` | Register, login, verification, password recovery, tokens |
| `/users` | User/profile/staff/enrollment-related data |
| `/courses` | Course template catalogue and management |
| `/course-instances` | Course delivery, enrollment, lesson completion, instance results |
| `/seminars` | Seminar template catalogue and management |
| `/seminar-instances` | Seminar delivery and enrollment |
| `/course-seminar-instances` | Shared instance queries and administration |
| `/assessment` | Assessments, exams, enrollment, results, practical submissions |
| `/certificates` | Administrator issuance and public certificate retrieval/share |
| `/programs` | Program catalogue, enrollment, progress, completion |
| `/categories` | Catalogue classification |
| `/payments` | Course/exam payment and approval |
| `/discount-codes` | Discount configuration and validation |
| `/reminders` | Reminder support |
| `/blog` and `/nfs/blog` | Blog content and files |
| `/contact`, `/seo` | Public support functions |

No active Study Group, Challenge, XP, Badge, Refresher, or gamification API route was found.

## 3. Authorization map

- `isAuthenticated` verifies an HS256 JWT and rejects refresh tokens on protected endpoints.
- `isOwner` compares the authenticated user ID with a `userId` path parameter.
- `isAdmin` requires `ADMIN`.
- `isAdminOrOwner` allows the administrator or matching user.
- `isAdminOrManager` allows `ADMIN`, `CONTENT_MANAGER`, or `TEACHER`.
- `isPrivateUser` supplies privacy context but is not an ownership check.

New gamification routes should derive learner identity from `req.user._id` whenever a learner acts on their own record. Staff overrides should use a separate authorized route and record the actor and reason.

## 4. Current trusted or potentially trusted sources

| Source | Current backend evidence | Integration assessment |
|---|---|---|
| Assessment result submission | Authenticated learner identity is derived from token | Strong source after normal validation |
| Quiz score/pass | Calculated and stored in `Assessment.results` | Strong source |
| Practical result | Staff/grader route protected by role middleware | Strong source with audit extension recommended |
| Practical submission | Authenticated identity, enrollment/window access, private file handling | Strong completion source; submission quality is not implied |
| Exam enrollment | Assessment enrollment exists; self-enrollment route explicitly checks identity | Strong state event |
| Successful Course completion | Service checks every attached exam and updates mirrored Course/User arrays | Strong business event; adapter should publish once |
| Certificate issuance | Administrator-only service validates all exams and writes Certificate | Strong event |
| Program progress/completion | Calculated from successfully completed Courses | Strong derived state |
| Lesson completion | Stored per lesson with timestamp | Usable for display only until route/idempotency hardening |
| Course/Seminar enrollment | Transaction updates mirrored records | Useful scope event; course route needs self-identity hardening |

## 5. Lesson-completion trust gap

Current route shape:

```text
PUT /course-instances/:courseInstanceId/lesson/:lessonId/complete/:userId
```

Observed problems:

1. The learner identity comes from `:userId`; the route does not use `isOwner` or replace it with the token subject.
2. The route does not visibly verify that the target learner is enrolled in the Course Instance.
3. The update uses `$addToSet` with `{ user, completedAt: new Date() }`. MongoDB compares the complete embedded object, so a replay with a new timestamp is not equal to the old object.
4. The route does not validate lesson order or whether an associated assessment was passed; those controls are mainly in the current frontend flow.

Required hardening before reward integration:

- derive the learner from `req.user._id` for self-service completion;
- verify Course Instance enrollment and lesson existence;
- enforce server-side completion rules;
- use a unique completion identity such as `(courseInstanceId, lessonId, userId)`;
- make repeated requests return the existing completion without adding another row;
- provide an authorized correction route rather than silently deleting evidence;
- publish one source event after the durable write succeeds.

## 6. Recommended event adapter boundary

Do not place XP or badge logic inside existing Course/Assessment services. Add a small adapter/outbox layer that records an event in the same logical transaction or through a reliable post-commit mechanism.

Minimum source-event fields:

- unique occurrence ID;
- event type;
- actor and learner IDs where relevant;
- Course, Course Instance, Assessment, lesson, Program, or Certificate IDs;
- occurrence time and recorded time;
- source service and rule version;
- correction/reversal reference;
- payload required to recompute eligibility.

Downstream progress, XP, achievements, challenges, and analytics should be independent consumers and idempotent by occurrence ID.
