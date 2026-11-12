# Architecture — Life OS V0.1

## 1. Architecture objective

Keep the first version small, local-first, explainable, and easy to rebuild. The UI should remain simple while the underlying model can grow gradually.

## 2. Logical components

```text
User input
   |
   v
Capture / Intent Router
   |
   +---- DO ------> Prioritisation Engine ------> Next-action response
   |
   +---- CHECK ---> Status Interpreter ---------> Adaptive summary
   |
   +---- LOG -----> Interpretation Layer -------> Preview -> Confirm/Edit
   |
   +---- MORE ----> Query / Search Layer --------> Answer from stored data
   |
   v
Life Graph (goals, actions, logs, preferences, relationships)
   |
   v
Storage Adapter (localStorage in V0.1)
```

These are logical boundaries. They do not require separate services or microservices.

## 3. Suggested modules

Even in a single HTML file, keep code grouped into functions or sections:

- `routeIntent(input)` — route user intent to DO, CHECK, LOG, or MORE.
- `interpretLog(input, context)` — produce a proposed structured log.
- `validateInterpretation(proposal)` — check required fields and uncertainty.
- `saveConfirmedLog(proposal)` — save only after explicit confirmation.
- `rankActions(actions, context)` — calculate a transparent priority score.
- `summariseStatus(data)` — produce a concise status summary.
- `detectPatterns(logs)` — identify simple repeated patterns.
- `findRelatedEntities(entity, graph)` — connect relevant goals and records.
- `loadState()` / `saveState(state)` — persistence boundary.
- `exportBackup()` / `importBackup(file)` — optional JSON backup.

## 4. Data model (starter)

Use stable IDs and ISO 8601 timestamps. Keep optional values nullable or absent.

### Goal

```json
{
  "id": "goal_001",
  "title": "Learn conversational Spanish",
  "description": "",
  "status": "active",
  "target": null,
  "unit": null,
  "deadline": null,
  "createdAt": "2026-01-01T10:00:00.000Z",
  "updatedAt": "2026-01-01T10:00:00.000Z"
}
```

### Action

```json
{
  "id": "action_001",
  "title": "Complete lesson 3",
  "status": "pending",
  "dueAt": null,
  "estimatedMinutes": 20,
  "importance": 3,
  "impact": 3,
  "goalIds": ["goal_001"],
  "createdAt": "2026-01-01T10:00:00.000Z"
}
```

### Log

```json
{
  "id": "log_001",
  "rawInput": "Practised Spanish for 20 minutes",
  "interpretedType": "practice",
  "structuredData": {
    "activity": "Spanish practice",
    "durationMinutes": 20
  },
  "occurredAt": "2026-01-01T10:00:00.000Z",
  "relatedGoalIds": ["goal_001"],
  "createdAt": "2026-01-01T10:01:00.000Z"
}
```

### Preference

```json
{
  "id": "preference_001",
  "statement": "Prefers short planning sessions",
  "source": "explicit",
  "confidence": 1,
  "createdAt": "2026-01-01T10:00:00.000Z"
}
```

### Relationship

```json
{
  "sourceId": "log_001",
  "targetId": "goal_001",
  "relationshipType": "supports"
}
```

These are illustrative starter schemas, not a requirement to expose every field in the UI.

## 5. Storage

V0.1 can use one versioned localStorage key, such as `lifeOS.data.v1`.

Recommended state shape:

```json
{
  "schemaVersion": 1,
  "goals": [],
  "actions": [],
  "logs": [],
  "preferences": [],
  "relationships": []
}
```

Implementation notes:
- Catch JSON parse and storage quota errors.
- Validate imported JSON before replacing current data.
- Keep a backup/export path.
- Do not store secrets.
- Explain that clearing browser data may erase local records.
- `localStorage` is not encrypted, synced, or a substitute for backups.

## 6. AI integration boundary

Keep model calls behind a provider-neutral function, for example:

```js
async function interpretWithAssistant(input, context) {
  // Replace with a secure server-side API call when available.
  // Do not put provider API keys in browser JavaScript.
}
```

The app should still work in a basic mode without an LLM. A rule-based parser can handle a limited set of explicit inputs, but it must not be described as a full AI system.

If adding a real LLM:
1. Create a backend or serverless function.
2. Store provider credentials in server-side environment variables.
3. Send only the minimum relevant context.
4. Validate model output against a schema.
5. Ask for confirmation before writing structured records.
6. Handle network failures and malformed responses.
7. Document privacy and retention implications.

## 7. Prioritisation approach

Start with a transparent heuristic, not opaque machine learning.

Potential factors:
- Deadline proximity
- Overdue status
- Explicit importance
- Expected impact
- Dependency blocking
- Estimated effort versus available time
- Connection to an active goal

Do not invent missing values. Use neutral defaults and show the reason behind the chosen action. Avoid allowing one arbitrary numeric score to become a substitute for user values.

## 8. Pattern detection

Begin with descriptive statistics:
- Frequency over a recent window
- Consecutive days/weeks, where appropriate
- Moving average, only when enough observations exist
- Change versus previous period
- Confidence / data sufficiency

Keep observed facts separate from forecasts. A pattern suggestion should be framed as a possibility, not certainty.

## 9. Privacy and safety

- Keep the initial app local-first.
- Do not include real personal data in public demo fixtures.
- Do not expose API keys in GitHub.
- Make data export and deletion possible.
- Do not present health-related pattern detection as diagnosis or medical advice.
