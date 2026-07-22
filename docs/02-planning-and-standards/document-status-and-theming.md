# Document Status and Theming

## 1. Document status

The feature documents in this repository are **rough functional outlines**.

They describe the intended purpose, main behavior, safeguards, dependencies, and representative acceptance criteria for each feature. They are not final product specifications or exact implementation instructions.

The following details remain provisional and may change during later product, UX, technical, and stakeholder review:

- feature names and learner-facing terminology;
- exact screens, layouts, navigation, and visual design;
- XP amounts, thresholds, limits, level curves, and reward values;
- challenge and achievement catalogues;
- permission details and moderation workflows;
- event names, model names, and technical structures;
- which behavior belongs in the first release;
- wording used for live and self-paced courses.

Acceptance criteria in these documents are representative of the important business rules. They are not intended to be a complete test suite.

## 2. Functional rules and presentation are separate

The requirements define what a feature must accomplish and which safeguards it must preserve. The final interface may present those mechanics using a different theme, metaphor, or visual language.

For example, a TTRPG-inspired presentation could represent:

| Functional concept | Possible themed presentation |
|---|---|
| Course | Campaign or adventure map |
| Course section | Region, chapter, or route |
| Lesson or activity | Location, encounter, or objective |
| Required progress | Main journey or campaign path |
| Optional progress | Exploration path or side content |
| Milestone | Checkpoint, landmark, or chapter completion |
| Study group | Adventuring party |
| Challenge | Quest |
| Optional exploration challenge | Side quest |
| Collaborative challenge | Party quest |
| Competitive challenge | Tournament, trial, or friendly contest |
| Post-course Knowledge Refresher | Revision challenge, memory trial, or return exercise |
| Future Skill Profile | Mastery map or skill record |
| Final-exam readiness | Preparation for the final encounter |
| Achievement or badge | Title, artifact, crest, or trophy |
| XP and level | Experience and rank |

These are examples rather than final naming decisions.

## 3. Theming safeguards

A theme should support motivation without making the LMS harder to understand.

The final design should therefore:

- keep required and optional work clearly distinguishable;
- use plain-language explanations alongside themed terminology where needed;
- remain accessible to learners unfamiliar with games or TTRPGs;
- avoid making serious academic information, deadlines, or exam requirements ambiguous;
- support localization and different course audiences;
- allow the visual theme to change without changing the underlying progress and reward rules.

The final theme and detailed content style should be decided after the functional feature set and catalogues are reviewed. The business requirements continue to use plain functional names such as Study Groups and Collaborative Challenges.
