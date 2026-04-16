# Initial Technical Architecture

## Objective

Build a fast, low-cost prototype that proves one thing:

A user's prior context can materially improve the interpretation of a new statement.

## Product slice to support

The first prototype should support this flow:

1. User creates a profile
2. User defines a few topic preferences and traits
3. User writes a few reflections
4. User submits a new statement
5. System retrieves relevant context
6. LLM produces a structured interpretation
7. User can correct the output
8. Corrections improve future interpretations

## Recommended stack

### Frontend
- **Next.js**
- **TypeScript**
- Simple authenticated UI
- Initial screens:
  - onboarding
  - topic profile editor
  - reflection journal
  - statement interpreter
  - correction review

Why:
- fast to ship
- good developer ergonomics
- easy API integration
- easy future deployment on Vercel or Azure Static Web Apps

### Backend
- **Next.js API routes** for MVP or a small **FastAPI** service if you want stricter separation

Recommended MVP path:
- start with Next.js full-stack
- split backend later only if orchestration complexity grows

### Relational storage
- **PostgreSQL**

Stores:
- users
- topic_profiles
- preferences
- reflections metadata
- statements
- interpretations
- user_corrections
- permissions metadata

Why:
- reliable
- flexible
- easy local and cloud deployment
- strong support for structured product evolution

### Vector retrieval
- **pgvector on PostgreSQL** for MVP

Stores embeddings for:
- reflections
- topic notes
- selected corrections

Why:
- simplest architecture
- avoids introducing a separate vector database too early
- enough for prototype-scale semantic retrieval

### LLM layer
- Model-agnostic orchestration layer with a single interpreter service

Responsibilities:
- build interpretation prompt
- retrieve relevant prior context
- generate structured JSON output
- store explanation trace

For MVP, the service should produce fields like:
- primary_topic
- emotional_intensity
- literalness
- conviction
- confidence
- interpretation_summary
- downstream_agent_recommendation

### Auth
- Lightweight auth only if needed in prototype
- If single-user early build, defer full auth
- If multi-user from day one, use a managed auth provider

### Deployment

#### Fastest path
- Frontend + API: Vercel
- Database: managed Postgres

#### If you want Azure alignment early
- Frontend: Azure Static Web Apps or App Service
- Backend: Azure App Service / Container Apps
- Database: Azure Database for PostgreSQL

For speed, I would still start with the fastest deploy path and move later.

## Logical components

### 1. Profile Service
Creates and updates user profile, topic profiles, and preferences.

### 2. Reflection Service
Stores long-form reflections and creates embeddings.

### 3. Context Retrieval Service
Given a new statement:
- identifies candidate topics
- retrieves semantically relevant reflections
- retrieves topic profile and preference evidence
- retrieves recent corrections

### 4. Interpretation Engine
Combines:
- statement
- topic profile
- relevant reflections
- user correction history

Outputs structured interpretation.

### 5. Correction Engine
Lets the user modify:
- topic
- literalness
- conviction
- emotional intensity
- summary

Stores correction data for future retrieval.

## Retrieval strategy for MVP

When a new statement arrives:

1. detect likely topic candidates
2. retrieve top matching reflections by semantic similarity
3. retrieve direct topic profile for that topic
4. retrieve prior corrections relevant to similar statements
5. generate one final interpretation with evidence trace

## Suggested API surface

### POST /profile/onboarding
Create initial user context

### POST /topics
Create or update a topic profile

### POST /reflections
Save reflection and embedding

### POST /interpret
Interpret a new statement

### POST /interpretations/:id/corrections
Store a user correction

### GET /interpretations/:id
Fetch interpretation plus evidence trace

## Suggested first schema notes

### topic_profiles
- id
- user_id
- topic_name
- interest_level
- emotional_charge
- expression_style
- default_literalness
- notes
- created_at
- updated_at

### reflections
- id
- user_id
- text
- source_type
- topic_hint
- embedding
- created_at

### statements
- id
- user_id
- text
- channel
- created_at

### interpretations
- id
- statement_id
- primary_topic
- emotional_intensity_score
- literalness_score
- conviction_score
- confidence_score
- interpretation_summary
- downstream_agent_recommendation
- raw_model_output
- created_at

### corrections
- id
- interpretation_id
- field_name
- previous_value
- corrected_value
- rationale
- created_at

## Product constraints to enforce

1. **Inspectable outputs**  
   The user must be able to see why the model produced an interpretation.

2. **Editable identity**  
   The user must be able to override inferred context.

3. **Private-by-default**  
   No external sharing in the MVP.

4. **No overclaiming certainty**  
   Confidence and ambiguity should be explicit.

## Recommended build order

### Step 1
Build manual onboarding + reflection capture + one-shot interpretation.

### Step 2
Add retrieval from prior reflections.

### Step 3
Add correction loop.

### Step 4
Add topic profile editing and evidence trace UI.

## My recommended MVP architecture decision

Use:
- Next.js
- TypeScript
- PostgreSQL + pgvector
- One interpreter service
- One clean JSON schema for output

This is the fastest credible path to validate the idea without overengineering.