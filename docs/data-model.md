# Data Model Draft

## Core entity groups

### 1. User
Represents the person and high-level profile metadata.

Fields:
- user_id
- display_name
- preferred_languages
- privacy_preferences
- created_at
- updated_at

### 2. TopicProfile
Represents context within a specific domain.

Examples:
- football
- work
- politics
- money
- family
- music

Fields:
- topic_id
- user_id
- topic_name
- interest_level
- emotional_charge
- expression_style
- default_literalness
- confidence
- notes

### 3. Preference
Represents a stable or semi-stable preference.

Fields:
- preference_id
- topic_id
- label
- affinity_direction
- intensity
- stability
- evidence_count

Examples:
- Tigres = strong positive
- Liverpool = medium positive
- Bayern = medium positive
- America = contextual negative in sports discourse

### 4. Reflection
User-authored longer-form context entry.

Fields:
- reflection_id
- user_id
- text
- source_type
- timestamp
- extracted_topics
- embedding_reference

### 5. Statement
A new text to interpret.

Fields:
- statement_id
- user_id
- text
- channel
- timestamp
- raw_topic_candidates

### 6. Interpretation
Machine output for a statement.

Fields:
- interpretation_id
- statement_id
- primary_topic
- emotional_intensity_score
- literalness_score
- conviction_score
- confidence_score
- interpretation_summary
- safety_recommendation
- generated_at

### 7. EvidenceLink
Connects an interpretation to prior context.

Fields:
- evidence_link_id
- interpretation_id
- source_type
- source_id
- relevance_weight
- explanation

### 8. UserCorrection
Lets the user refine the model.

Fields:
- correction_id
- interpretation_id
- correction_type
- previous_value
- corrected_value
- explanation
- timestamp

## Important modeling concepts

### Literalness
How literally a statement should be interpreted.

### Conviction
How deeply the statement reflects a stable belief.

### Emotional intensity
How emotionally charged the statement is in the moment.

### Stability
How persistent a preference or position is over time.

### Topic-specific language mode
The same person may be formal in work and exaggerated in sports.

## Suggested first schema approach

A relational core plus a vector layer for reflection retrieval.

- relational DB for users, topics, statements, interpretations, corrections
- vector store for semantically retrieving relevant reflections and context
