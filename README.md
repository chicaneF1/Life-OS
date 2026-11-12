# Life OS — The AI-Powered Personal Execution System

> A lightweight personal operating system that helps turn natural-language thoughts and updates into clear next actions, meaningful progress, and better decisions.

**Status:** V0.1 prototype / evolving personal project  
**Deployment target:** GitHub Pages  
**Initial build approach:** Single-page web application with local-first persistence

---

## 1. The problem

People often have goals, notes, tasks, habits, reminders, and information scattered across different tools. The hard part is not simply storing more information: it is understanding what matters now, deciding what to do next, and learning from what has happened.

Life OS is designed around that execution gap.

It aims to reduce the cognitive effort required to organise life. The user should be able to describe what they need or what happened in ordinary language. The system should interpret that input, create a useful structure, and present only the information that helps the user act.

## 2. Product philosophy

- **Execution over information storage.** Life OS is not intended to replace OneNote, Notion, or a general-purpose knowledge repository.
- **Natural language first.** Users should not need to classify every input as a task, habit, goal, project, or log.
- **Automatic by default, editable by choice.** The system proposes structure; the user retains control.
- **Start simple; add structure only when useful.** Do not turn every intention into a complicated goal-management system.
- **Low cognitive load.** Show the smallest useful amount of information.
- **Adaptive intelligence.** Begin conservatively and learn from explicit preferences and repeated user choices.
- **Explain important recommendations.** The system should briefly communicate why it recommends an action.
- **No silent saves.** Show the interpreted entry and ask the user to confirm or edit it before saving.

## 3. Core interaction

The opening screen is a neutral gateway. It does not assume what the user wants to do.

**What do you need right now?**

1. **DO** — What should I do now?
2. **CHECK** — How am I doing, and what needs attention?
3. **LOG** — What happened?
4. **More** — Search, explore, or ask Life OS anything.

A natural-language input should be available so the user can describe their need directly.

### DO — decide the next action

Show one best next action, with a short reason and estimated effort/time where known. Below it, show only other urgent or pending actions and goals that genuinely need attention.

The prioritisation logic may consider:
- Importance and urgency
- Expected impact and consequences
- Deadlines and dependencies
- User-stated priorities
- Available time and context
- Effort and estimated duration
- Repeated user preferences and choices

The user should not have to operate an Eisenhower matrix or manually rank every item.

### CHECK — interpret status

Answer: **“How is my life doing, and what needs my attention?”**

Use an adaptive summary. If nothing important needs attention, keep the response short. If something is falling behind, identify it and explain why. Do not display every metric, goal, chart, or log just because it exists.

### LOG — capture what happened

Accept natural-language entries by text or voice input (voice is optional and may depend on browser capabilities).

Example:

> “Ran 10 km today.”

Show the interpretation before saving:

- Activity: Running
- Distance: 10 km
- Date: Today
- Relevant goal or pattern, if confidently identified
- Optional comparison, such as last run or recent average
- A caution if the pattern may need a break or recovery

Actions: **Confirm** or **Edit**.

Life OS may identify patterns and suggest a next step, but it must not blindly extrapolate a pattern when doing so could be harmful or misleading.

### More — universal search and exploration

More is not a large module drawer. It is a universal gateway for requests such as:
- “Show my running goals.”
- “What systems have I created?”
- “Show logs from September.”
- “Why am I falling behind?”
- “What do you know about my preferences?”

## 4. Core product model

Life OS uses a connected **Life Graph** concept underneath the interface. This is an internal model, not a navigation screen.

Possible connected objects include:
- Goals and intentions
- Actions and commitments
- Logs and events
- Patterns and routines
- Measurements and progress
- People and relationships
- Resources and relevant references
- Preferences, decisions, context, and reviews

The user should not have to understand or manage this graph directly. The system creates relationships when useful and keeps the interface simple.

### Life dimensions

The system may use these dimensions as a lens for interpretation and review, not as mandatory categories:

- Fun
- Mind
- Career
- Money
- Body
- People
- Purpose
- Daily Life

An item may relate to more than one dimension. Users should never be forced to classify every entry.

## 5. V0.1 scope

### Build first
- Neutral opening gateway
- DO, CHECK, LOG, and More
- Natural-language capture
- Interpretation preview with Confirm and Edit
- Basic goals, actions, logs, and relationships
- Simple pattern detection based on recorded data
- Minimal prioritisation logic with explainable reasons
- Local persistence (for example, `localStorage`)
- Basic edit and delete controls
- Responsive, accessible interface

### Explicitly out of scope for V0.1
- A large dashboard full of scores and charts
- A full knowledge-management or wiki system
- A resource vault
- Complex habit-management screens
- A focus timer as the primary workflow
- WhatsApp or Microsoft To Do integrations
- Elaborate dimension-management UI
- Complex settings and customisation
- Multi-user collaboration or cloud sync unless added as a later requirement

## 6. Suggested technology approach

The initial prototype should remain intentionally simple.

| Layer | V0.1 recommendation | Notes |
|---|---|---|
| UI | HTML, CSS, vanilla JavaScript | A single-page app is sufficient for the first prototype |
| Persistence | `localStorage` | Suitable for a single-user prototype; not a secure backup or sync system |
| Hosting | GitHub Pages | Static hosting for the front end |
| AI interpretation | Optional LLM API integration | Keep behind a replaceable service layer; never expose secret API keys in browser code |
| Testing | Browser testing + unit tests for pure logic | Test interpretation, prioritisation, and persistence separately |

No third-party runtime dependency is required for a basic single-file prototype. If the project later adopts React, TypeScript, a backend, or an AI provider, document the exact versions and setup commands in the repository.

**Security note:** GitHub Pages serves static files. Do not put private API keys, passwords, or sensitive personal data in source code or public repositories. A production AI integration should call a protected backend or serverless function.

## 7. Suggested repository structure

```text
life-os/
├── README.md
├── prompts/
│   └── GEMINI_BUILD_PROMPT.md
├── docs/
│   ├── PROJECT_SUMMARY_PROMPT.md
│   ├── ARCHITECTURE.md
│   └── REBUILD_GUIDE.md
├── index.html                 # application entry point (when implemented)
├── assets/                    # optional images, icons, styles
└── .gitignore
```

For the first prototype, `index.html` can contain the HTML, CSS, and JavaScript. Split files only when the code becomes difficult to maintain.

## 8. Run locally

If the project is a single static HTML file:

1. Clone or download the repository.
2. Open `index.html` in a modern browser.

For a more reliable local server, run:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## 9. Deploy with GitHub Pages

1. Push the project to a GitHub repository.
2. Open **Settings → Pages**.
3. Under the build and deployment section, choose **Deploy from a branch**.
4. Select the branch (usually `main`) and folder (`/root`).
5. Save and wait for the deployment to complete.
6. Open the published URL shown in the Pages settings.

If the application uses a build tool in a later version, configure the appropriate build output folder instead.

## 10. Product principles for future contributors

Before adding a feature, ask:

1. Does this help the user decide, act, understand progress, or learn?
2. Does it reduce cognitive load rather than add another management burden?
3. Can the system infer or create the structure instead of asking the user to configure it?
4. Is this information relevant to something active?
5. Can the feature remain hidden until it is useful?

If a feature does not improve execution or understanding, it probably does not belong in the core product.

## 11. Current implementation status

This repository documentation describes the intended product and a rebuildable V0.1 specification. It does **not** claim that every described capability is already implemented. Update this section as the actual code is built and tested.

| Capability | Intended V0.1 status |
|---|---|
| Neutral gateway | Build |
| DO / CHECK / LOG / More | Build |
| Natural-language capture | Build |
| Confirm-before-save interpretation | Build |
| Basic goal/action/log storage | Build |
| Pattern recognition | Basic, rule-based first |
| AI/LLM integration | Optional; only claim once implemented |
| Local persistence | Build |
| GitHub Pages deployment | Deployment target |

## 12. License

Choose a license before inviting external contributions. If this is a personal project, you can initially keep the repository private or add a license later.
