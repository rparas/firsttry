# Prototype App Spec

## Product name for working purposes

Personal Context Engine

## Prototype goal

Demonstrate that AI can interpret a user's new statement more accurately when it has access to structured personal context and prior reflections.

## User promise

"Build a context profile so AI can read you with more nuance."

## Primary user

A heavy AI user who writes often, thinks in nuances, and wants better alignment between what they mean and how systems interpret them.

## Prototype scope

Single-user or light multi-user prototype.

No public feed, no social graph, no external integrations required.

## Core user journey

### 1. Onboarding
The user answers a short set of prompts such as:
- what topics matter to you most?
- how do you usually speak about those topics?
- in what topics are you more emotional or exaggerated?
- what kinds of statements should not be interpreted literally?
- what preferences feel stable vs casual?

### 2. Topic setup
The user creates a few topic cards:
- football
- work
- money
- family
- politics
- entertainment

Each topic card can include:
- interest level
- emotional charge
- style of expression
- important entities
- notes for interpretation

### 3. Reflection capture
The user writes a few reflections or notes.

Examples:
- "Tigres is my favorite team"
- "I enjoy Liverpool and Bayern but less intensely"
- "In football I exaggerate and vent"
- "Do not treat my sports reactions as deep moral positions"

### 4. Statement interpretation
The user pastes a new statement.

Example:
`Que chingue a su madre el America`

The system returns:
- topic: football
- emotional intensity: high
- literalness: low
- conviction: medium-low
- confidence: medium-high
- interpretation summary
- evidence trace
- downstream agent recommendation

### 5. Correction
The user can adjust the output.

Examples:
- lower conviction
- mark as more emotional than literal
- edit summary
- add note for future interpretations

## Screens

### Screen 1 — Home
Purpose:
- explain what the product does
- entry points to onboarding, reflections, and interpreter

### Screen 2 — Onboarding
Purpose:
- collect initial user context

### Screen 3 — Topic Profiles
Purpose:
- manage topic-specific preferences and interpretation rules

### Screen 4 — Reflection Journal
Purpose:
- store long-form context and notes

### Screen 5 — Statement Interpreter
Purpose:
- accept new text
- display structured interpretation

### Screen 6 — Interpretation Detail
Purpose:
- show explanation trace
- show supporting reflections and topic data
- allow corrections

### Screen 7 — Corrections History
Purpose:
- let the user inspect and manage how the system has learned from corrections

## Functional requirements

### FR1
The user can create and edit a topic profile.

### FR2
The user can save free-form reflections.

### FR3
The system can interpret a new statement using retrieved context.

### FR4
The system returns a structured JSON plus a human-readable summary.

### FR5
The user can correct the interpretation.

### FR6
Future interpretations can use prior corrections as evidence.

## Non-functional requirements

### NFR1
Response time for interpretation should feel interactive.

### NFR2
The system should show uncertainty explicitly.

### NFR3
The system should be private by default.

### NFR4
The system should be inspectable and explainable.

## Initial interpretation schema

```json
{
  "primary_topic": "football",
  "emotional_intensity": 0.88,
  "literalness": 0.18,
  "conviction": 0.42,
  "confidence": 0.79,
  "interpretation_summary": "The statement is best interpreted as emotional sports venting rather than a literal or deeply held hostile belief.",
  "downstream_agent_recommendation": "Treat as colloquial rivalry language in a football context. Do not classify as threat or core moral stance.",
  "evidence": [
    {
      "type": "reflection",
      "label": "User says he exaggerates in football"
    },
    {
      "type": "preference",
      "label": "Tigres is favorite team"
    }
  ]
}
```

## Prototype success metrics

### Qualitative
- user says the system interpreted them better than a generic AI would
- user understands why the output was produced
- user sees value in correcting the system

### Quantitative
- onboarding completion rate
- number of reflections entered
- number of statements interpreted
- number of corrections per user
- percentage of interpretations accepted without major edits

## What the prototype is not trying to prove yet

- broad social adoption
- full identity graph portability
- public reputation use cases
- enterprise-grade compliance
- external API ecosystem

## Best demo scenario

1. Create a user profile
2. Add football preferences and notes
3. Add 2 or 3 reflections
4. Paste a sports rant
5. Show interpretation with context trace
6. Correct one field
7. Re-run a similar statement and show improvement
