# Personal Context Engine

A product exploration to build a personal context and identity interpretation layer for AI agents.

## Core idea

Humans do not speak in clean, literal, machine-ready statements. We speak with emotion, irony, exaggeration, contradiction, and cultural context. Future AI agents will need more than memory about us; they will need a structured way to interpret what we mean.

This project explores a system where a person can build and maintain a living map of:

- preferences
- values
- emotional intensity by topic
- communication style
- stable convictions vs momentary reactions
- public vs private context
- interpretation rules for AI agents

Example:

If a user writes: `Que chingue a su madre el America` after a Tigres match, an AI without context may misread that as hate speech or deep hostility. An AI with contextual identity data may interpret it as:

- topic: football
- tone: emotional
- literalness: low
- conviction level: medium-low
- cultural mode: colloquial sports expression
- recommendation: do not treat as a literal threat or core moral position

## Working thesis

The future digital economy will need a new layer between raw user expression and AI interpretation.

This project calls that layer **Personal Context Engine**.

## Repo structure

- `docs/vision.md` — long-form vision and category definition
- `docs/problem-statement.md` — problem, users, and jobs to be done
- `docs/mvp.md` — first product cut and scope
- `docs/data-model.md` — core entities and interpretation model
- `docs/roadmap.md` — staged roadmap
- `docs/open-questions.md` — critical unresolved questions

## Phase 1 goal

Define a credible MVP that can:

1. build a profile of user context by topic
2. classify new statements by tone, literalness, conviction, and emotionality
3. provide an interpretation summary for an AI agent
4. allow the user to correct and refine the model

## Product directions

Possible category names:

- Personal Context Engine
- Identity Interpretation Layer
- Human Meaning Engine
- Intent Graph
- Self Protocol

## Initial principle

The system should not primarily infer identity from external social data.

It should start from:

- user-declared context
- user corrections
- long-form reflections
- topic-based memory
- transparent and revisable interpretation

## Success criteria for the first milestone

- A clear problem statement
- A usable MVP definition
- A simple data model
- A first technical architecture proposal
- A set of concrete product questions and experiments
