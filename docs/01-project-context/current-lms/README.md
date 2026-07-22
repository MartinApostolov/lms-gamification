# Detailed Current LMS Maps

This folder contains the expanded current-state analysis produced after reviewing the complete LMS mock-up.

## Documents

- [Entity Relationship Map](entity-relationship-map.md) — model relationships, embedded learning evidence, mirrored data, and dormant entities.
- [Domain and Workflow Map](domain-and-workflow-map.md) — catalogue, delivery, assessment, completion, certificate, program, payment, and reminder workflows.
- [Frontend and Role Map](frontend-and-role-map.md) — learner/staff routes, role boundaries, and natural integration points for gamification.
- [Backend and API Map](backend-and-api-map.md) — route families, authorization, current source events, and trust risks.
- [Gamification Integration Assessment](gamification-integration-assessment.md) — what can be reused now, what needs hardening, and what must be added.
- [Source Evidence Index](source-evidence-index.md) — principal code paths supporting the map.

## Interpretation rule

A schema field proves that data can be stored, but it does not by itself prove the complete business workflow. A frontend display proves that a screen exists, but not that the backend accepts it as trusted evidence. Reward-capable conclusions therefore prioritize backend-enforced, identity-bound, idempotent events.
