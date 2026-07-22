# Source Note

## Evidence reviewed

The original current-state analysis was based on eight exported Mongoose models. The analysis has now been updated using the complete supplied LMS mock-up source package, `interns-lms-main.zip`.

The reviewed snapshot includes:

- the React front end in `lms-fe`;
- the Node/Express/Mongoose back end in `lms-be`;
- 17 Mongoose model files;
- controllers, services, routes, authentication and authorization middleware;
- local seed data and test accounts;
- assessment, exam, payment, certificate, program, course, and seminar flows;
- Bulgarian and English translation files;
- the existing gamification activity-tracker placeholder.

The package is a deliberately local training copy rather than the production platform. Findings describe the supplied mock-up and must not be presented as claims about a production deployment.

## Evidence labels

The Current LMS Map uses these labels:

- **Confirmed — model:** directly represented by a Mongoose schema.
- **Confirmed — backend:** enforced or calculated by a controller, service, middleware, or route.
- **Confirmed — frontend:** visible in a React route or component.
- **Seeded:** demonstrated by the supplied local seed data, but not necessarily a universal business rule.
- **Placeholder:** present only as non-functional or synthetic demonstration UI.
- **Dormant/legacy:** a schema or component exists but no active route or main workflow was found in the reviewed snapshot.
- **Inferred:** a reasonable interpretation that is not directly enforced by the source.

## Review boundary

The review was static. The application was not treated as authoritative production behavior, and no production database, external service, email provider, payment provider, or deployment configuration was accessed.

Code paths are included throughout the map so implementation teams can verify each conclusion against the supplied snapshot.
