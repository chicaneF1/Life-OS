# Rebuild and Development Guide

This guide describes how to recreate Life OS V0.1 from scratch.

## 1. Minimum requirements

For the simplest prototype:
- A modern browser
- A text editor or IDE
- Git and a GitHub account
- A static HTML/CSS/JavaScript project

No framework or package manager is required for a single-file prototype.

## 2. Recommended build sequence

### Step 1 — Create the shell
Create `index.html` with:
- Semantic HTML
- Embedded or separate CSS
- JavaScript entry point
- Responsive layout
- Neutral gateway as the initial screen

Do not start with a dashboard.

### Step 2 — Add the four routes
Implement:
- DO
- CHECK
- LOG
- MORE

Initially use small, clearly separated functions and simple placeholder states. Do not add extra modules.

### Step 3 — Add the data layer
Implement a versioned localStorage adapter:
- Load initial state
- Save changes
- Handle invalid or missing data
- Export/import JSON
- Add basic edit/delete operations

### Step 4 — Add natural-language capture
Start with a text input. Add speech-to-text only if browser support and user experience justify it.

Build an interpretation pipeline:
1. Receive raw input.
2. Detect likely intent.
3. Extract only information supported by the input.
4. Identify uncertainty or missing fields.
5. Show a preview.
6. Confirm or edit.
7. Save after confirmation.

### Step 5 — Add basic intelligence
Implement deterministic first versions of:
- Action ranking
- Goal/action relationships
- Status summary
- Pattern detection

Keep each function testable and explainable.

### Step 6 — Add an LLM only if needed
An LLM can improve natural-language interpretation and contextual reasoning, but it requires a secure server-side integration. Never place an API key in a public GitHub repository or static front-end bundle.

### Step 7 — Test the acceptance criteria
Use the checklist below before deployment.

## 3. Acceptance checklist

- [ ] First load opens the neutral gateway.
- [ ] DO, CHECK, LOG, and More are available.
- [ ] User can submit a natural-language entry.
- [ ] Interpretation is shown before saving.
- [ ] Confirm saves; Edit changes the proposed data.
- [ ] Refreshing the page preserves confirmed data.
- [ ] User can edit and delete saved records.
- [ ] DO shows one best action or honestly reports insufficient data.
- [ ] CHECK is concise and does not dump all data.
- [ ] More searches the user's stored information.
- [ ] Patterns distinguish observations from predictions.
- [ ] Uncertain interpretation asks for clarification.
- [ ] App works at mobile and desktop widths.
- [ ] No secrets or real personal data are committed.

## 4. Optional tools and dependencies

| Need | Lightweight option | When to add |
|---|---|---|
| UI framework | Vanilla HTML/CSS/JS | Start here; add React only if complexity warrants it |
| Type safety | TypeScript | When the data model and codebase grow |
| Build tooling | Vite | When using modules, React, or TypeScript |
| Styling | Plain CSS | Start here; add a CSS framework only if useful |
| Icons | Inline SVG or a small icon library | Only if needed |
| Unit testing | Vitest | When core logic is split into modules |
| Browser testing | Playwright | When workflows need repeatable end-to-end tests |
| AI | LLM API through backend | When deterministic parsing is insufficient |
| Backend | Serverless function / small API | Required for secure API credentials and shared sync |
| Database | IndexedDB, then hosted database if needed | When localStorage becomes limiting |

Do not install all of these at the start. They are options, not required dependencies.

## 5. Suggested future migration path

1. Single HTML file + localStorage.
2. Split into modules and add tests.
3. Add TypeScript/Vite if code size warrants it.
4. Add IndexedDB if data volume or structured querying requires it.
5. Add secure backend + LLM provider if real AI reasoning is required.
6. Add authentication/cloud sync only if multi-device use becomes a real requirement.

## 6. GitHub Pages deployment

For a static app:
1. Push `index.html` and assets to the repository.
2. Open repository Settings → Pages.
3. Choose Deploy from a branch.
4. Select `main` and `/root`.
5. Save and open the published URL after deployment.

If using Vite or another build tool later, configure GitHub Pages to publish the generated build output using an appropriate GitHub Actions workflow.
