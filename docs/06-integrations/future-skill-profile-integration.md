# Future Skill Profile Integration

> **Document status:** This is an integration boundary and future-direction note, not a complete Skill Profile business requirement or an implementation commitment.

## 1. Purpose

A future Skill Profile may summarize skills that a learner has demonstrated and use that information to recommend appropriate courses, challenges, or review activity.

The current gamification project should remain compatible with such a feature without duplicating the full Skill Profile work.

## 2. Possible future capabilities

A separate Skill Profile system may eventually support:

- a shared skill taxonomy;
- learner skill mastery or confidence levels;
- evidence sources and evidence dates;
- skill expiry or reduced confidence over time;
- course prerequisite and outcome skills;
- recommended next courses;
- diagnostic or assessment-first course entry;
- reduced self-paced course requirements for reliably demonstrated prior knowledge;
- targeted review when retained knowledge has weakened.

## 3. Current project integration points

### 3.1 Collaborative Challenges

A challenge definition may optionally reference:

- skills practised by the activity;
- skills demonstrated by successful completion;
- the evidence strength associated with an individual contribution or result.

Challenge completion must not automatically prove mastery unless a trusted evaluation rule supports that conclusion.

### 3.2 Post-course Knowledge Refreshers

A refresher may expose:

- topic or skill identifier;
- evaluated result;
- evidence date;
- related course and course version;
- question or activity version;
- confidence or evidence-strength metadata where available.

The refresher feature records results. The Skill Profile decides how those results affect mastery.

### 3.3 Course recommendations

The LMS may later combine:

- demonstrated skills;
- missing prerequisites;
- learner goals;
- completed courses;
- course difficulty and outcomes;
- recent refresher results.

The current project does not define the recommendation algorithm.

### 3.4 Adaptive self-paced course paths

A future self-paced course may offer:

1. a standard path with normal required activities;
2. a reduced path where approved activities are skipped after reliable diagnostic evidence;
3. an assessment-first path where the learner attempts a diagnostic or final assessment before choosing content;
4. a targeted review path containing only weak or missing skill areas.

Any reduction of required activities must be transparent, course-approved, auditable, and based on reliable evidence. A Skill Profile value by itself must not silently grant course completion, a certificate, or exam eligibility.

## 4. Minimum data contract

Where implemented, integrations should use stable identifiers and include:

- learner identifier;
- skill identifier and taxonomy version;
- evidence source type;
- source occurrence identifier;
- related course, course instance, challenge, refresher, or assessment;
- result or evidence value;
- evidence time;
- rule or evaluation version;
- correction or revocation relationship.

Processing must be idempotent so the same result does not create duplicate evidence.

## 5. Safeguards

- Learners should be able to understand why a course or activity was recommended.
- A low or old skill estimate should not publicly label or shame the learner.
- Skill information is private by default.
- Staff overrides and evidence corrections must be auditable.
- Skill evidence should distinguish practice, completion, assessment, and verified mastery.
- Stale evidence may lower confidence but should not erase historical accomplishments.
- Mandatory course, attendance, certification, or legal requirements cannot be skipped merely because a profile score is high.
- The learner should retain access to skipped self-paced content for optional review.

## 6. Out of scope for this project

The current implementation does not include:

- creation or governance of a full skill taxonomy;
- calculation of mastery scores;
- AI-generated skill evaluation;
- automatic course recommendation ranking;
- adaptive course-authoring tools;
- automatic reduction of required activities;
- diagnostic assessment design;
- cross-institution skill verification.

## 7. Integration acceptance criteria

### AC1 — Optional skill references

Given a Collaborative Challenge or Knowledge Refresher is configured with skill identifiers,
when a valid result is produced,
then the source may expose an idempotent skill-evidence event without requiring a Skill Profile to exist.

### AC2 — No automatic academic credit

Given skill evidence indicates high prior mastery,
when no approved adaptive course rule and reliable assessment exist,
then required course progress, completion, certificate status, and exam eligibility remain unchanged.

### AC3 — Correction

Given a challenge, refresher, or assessment result is corrected,
when skill evidence has already been consumed,
then a correction or revocation event can identify the original evidence occurrence.

### AC4 — Explainability

Given a future course recommendation uses Skill Profile data,
when it is shown to the learner,
then the interface should provide an understandable reason such as a demonstrated prerequisite or a missing skill area.
