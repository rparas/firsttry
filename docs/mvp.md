# MVP Definition

## MVP goal

Create a product prototype that can ingest user-authored reflections and return context-aware interpretations of new statements.

## MVP user promise

"Teach your AI how to read you better."

## Inputs

- manual user onboarding answers
- personal reflections or journal-style entries
- topic preferences entered by the user
- user corrections on past interpretations

## MVP outputs

For any new statement, the system returns:

- topic classification
- emotional intensity
- literalness score
- conviction score
- confidence score
- interpretation summary
- relevant prior context

## Example output

### Statement
`Que chingue a su madre el America`

### Interpreted output
- topic: football
- emotional intensity: high
- literalness: low
- conviction: medium-low
- likely mode: sports venting / tribal expression
- recommendation for agent: interpret as colloquial rivalry, not as a stable moral belief or credible threat

## Core MVP features

1. **Topic Profiles**  
   Build a context profile per domain such as football, work, politics, money, family, or entertainment.

2. **Statement Interpreter**  
   Analyze new user statements through the lens of the user context profile.

3. **User Correction Loop**  
   Let the user confirm, reject, or refine the interpretation.

4. **Context Traceability**  
   Show which previous reflections or declared preferences influenced the interpretation.

5. **Private-first storage**  
   Keep the raw user profile private by default.

## Out of scope for MVP

- full social media ingestion
- multi-agent API platform
- external enterprise integrations
- public sharing marketplace
- autonomous decision-making by agents

## Key product question

Will users find enough value in better interpretation to invest time in building their context profile?
