# Gemini Canvas Build Prompt — Life OS V0.1

You are building a functional, responsive web application called **Life OS — The AI-Powered Personal Execution System**.

Do not build a generic productivity dashboard. Do not reproduce a large cockpit, habit tracker, knowledge wiki, or task-management suite. The product's defining goal is to reduce cognitive load and help a person understand what matters and what to do next.

## Product philosophy

- Execution over information storage.
- Natural-language first.
- Automatic by default, editable by choice.
- Start simple; add structure only when useful.
- Keep the interface minimal and progressively disclose detail.
- Explain important recommendations briefly.
- Never silently save an interpreted log; always show a preview and ask for confirmation.
- The user interacts with life; the application manages the underlying structure.

## Primary opening screen

Always start with the neutral gateway. Do not attempt a personalised or time-aware greeting in V0.1 because the application may have no history or data yet.

Display:

**What do you need right now?**

- **Do something**
- **See how things are going**
- **Log something**
- A natural-language input: “Or just tell me what you need.”
- A subtle **More** option

Keep the screen calm, uncluttered, and visually restrained. Avoid a large sidebar or a grid of modules. Use no more than three prominent actions at once. Make secondary actions visually quieter.

## The four interaction routes

### 1. DO — What should I do now?

Show:
1. One best next action.
2. A short explanation of why it matters.
3. Estimated time/effort only when available.
4. Other urgent or pending actions, if any.
5. Goals needing attention, only when relevant.

Do not make the user fill in an Eisenhower matrix or manually rank tasks.

For V0.1, implement a transparent rule-based priority score using available fields such as importance, urgency, impact, deadline, effort, and dependency. If data is missing, do not fabricate it. Show a short reason for the recommendation.

### 2. CHECK — How am I doing?

Create an adaptive summary, not a dashboard.

If there is no important issue, say something like:
“You’re on track. Nothing important needs your attention.”

If there are issues, summarise only the most important ones, for example:
“Two things need attention. One action is overdue and one goal is falling behind.”

Do not display all goals, metrics, charts, and logs by default. Provide a way to inspect details when the user asks.

### 3. LOG — What happened?

Allow a user to type a natural-language update.

Example input:
“Ran 10 km today.”

Interpret the input and show a review card:
- What the user said
- What the application understood
- Relevant entity or activity
- Quantity and unit, if present
- Date/time, if understood
- Related goal or pattern, if confidently matched
- Optional comparison
- A warning if the pattern may be excessive or a break/recovery may be appropriate

Always provide:
- **Confirm**
- **Edit**

Do not save until the user confirms. If interpretation is uncertain, ask one concise clarification rather than inventing details.

For the first version, use simple deterministic parsing/rules where possible. Keep the interpretation logic behind a replaceable interface so an LLM can be connected later.

### 4. MORE — Universal search/explore

More must open a universal natural-language search/explore input, not a module drawer.

Support queries such as:
- “Show my running goals.”
- “What systems have you created?”
- “Show logs from September.”
- “Why am I falling behind?”
- “What do you know about my preferences?”

If a query cannot be answered from stored data, say so clearly.

## Underlying data model

Keep the data model minimal but extensible. Start with these entities:

- `Goal`: id, title, description, status, target, unit, deadline, createdAt, updatedAt
- `Action`: id, title, status, dueAt, estimatedMinutes, importance, impact, goalIds, createdAt
- `Log`: id, rawInput, interpretedType, structuredData, occurredAt, relatedGoalIds, createdAt
- `Preference`: id, statement, source (`explicit` or `inferred`), confidence, createdAt
- `Relationship`: sourceId, targetId, relationshipType

Do not force users to create all these entity types. Infer/create only what is useful. Store optional fields as optional. Use stable IDs.

## Pattern recognition

Implement simple, explainable patterns first:
- Repeated activity frequency
- Recent trend or streak
- Comparison with a recent average when enough data exists
- Missing data / insufficient evidence

Do not make medical claims or recommend unsafe extrapolations. If the data suggests overtraining or poor recovery, use cautious wording and recommend considering rest rather than automatically scheduling more activity.

Pattern output should distinguish:
1. What has been observed
2. What may happen next
3. When the pattern may need to be broken

Never present a prediction as a fact.

## Life dimensions

These are optional interpretation lenses, not required categories:
Fun, Mind, Career, Money, Body, People, Purpose, Daily Life.

An entry may relate to multiple dimensions. Do not ask users to classify every input. Do not make dimensions a primary navigation system.

## Persistence and editing

- Persist user data locally using `localStorage` for V0.1.
- Support create, read, update, and delete for the basic records.
- Add a clear way to edit or delete an item.
- Add a simple export/import JSON backup if feasible.
- Handle empty state gracefully.
- Do not seed the user's real personal data. If demo data is useful, make it clearly labelled and removable.
- The neutral gateway must remain the default opening screen even when demo data exists.

## Design requirements

- Minimal, calm, modern interface.
- Mobile-responsive and desktop-friendly.
- Strong visual hierarchy; one main action at a time.
- Very few icons.
- No decorative charts or scores without a clear decision-making purpose.
- Avoid dense cards, excessive colour, and permanent navigation clutter.
- Accessible labels, keyboard navigation, and adequate contrast.
- Use progressive disclosure for detail.

## Technical requirements

- Prefer a single self-contained `index.html` with embedded CSS and JavaScript for the initial prototype, unless the environment strongly favours a component framework.
- Do not add libraries or dependencies without a clear reason.
- Separate core logic into understandable functions even if the app is in one file.
- Keep parsing, prioritisation, pattern detection, storage, and UI rendering logically separate.
- Do not put API secrets in client-side code.
- If an LLM is integrated, use a secure backend/proxy. If no backend is available, clearly label AI integration as a future extension and do not pretend rule-based parsing is an LLM.

## Required acceptance tests

1. On first load, the neutral gateway appears.
2. A user can enter a natural-language log.
3. The app displays an interpretation preview.
4. Nothing is saved before Confirm.
5. Edit changes the proposed interpretation.
6. Confirm saves the log and it remains after refresh.
7. The user can inspect and delete the saved log.
8. DO returns one best action or explains that there is not enough information.
9. CHECK returns a concise status summary rather than a dashboard dump.
10. More accepts a natural-language query and searches available data.
11. Empty and uncertain states are handled honestly.
12. The layout works on mobile and desktop.

Build the working application, not just a static mock-up. After building, explain:
- Files created
- How to run locally
- How persistence works
- What is rule-based versus genuinely AI-powered
- Any features not yet implemented
- How to deploy to GitHub Pages
