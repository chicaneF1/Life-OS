# Life OS — Project Summary / Rebuild Context Prompt

Use this file as the context prompt when asking another AI assistant to understand, continue, rebuild, or improve this project.

---

You are helping me build **Life OS — The AI-Powered Personal Execution System**.

## What it is

Life OS is a personal execution layer. It helps me translate natural-language thoughts, intentions, and updates into useful structure, decide what deserves attention, understand progress, and learn from recurring patterns.

It is not primarily:
- A task manager
- A habit tracker
- A journal
- A knowledge-management system
- A dashboard
- A focus timer

It may contain some of those capabilities when they support the core purpose, but none should dominate the product.

## The problem it solves

Information and intentions are fragmented across tools. The user often knows many things they could do, but struggles to determine what matters now and convert information into consistent action.

Life OS should reduce the gap between knowing and doing.

## Non-negotiable design principles

1. Minimum cognitive load.
2. Natural-language-first interaction.
3. Automatic structure by default; user can edit or override.
4. Start simple and add complexity only when useful.
5. Explain important recommendations.
6. Never silently save interpreted logs.
7. Be conservative when evidence is weak.
8. Learn explicit preferences immediately; infer behavioural preferences only after repeated evidence.
9. Challenge meaningful bad trade-offs respectfully, but leave the decision to the user.
10. Do not show information merely because it exists.

## Opening screen

Always show the neutral gateway in V0.1:

**What do you need right now?**

- Do something
- See how things are going
- Log something
- Or just tell me what you need
- Subtle More

Do not replace this with a personalised greeting or dashboard in V0.1.

## Core interactions

### DO
Answer: “What should I do now?”
Return one best next action, a brief reason, and estimated time/effort if known. Then show only relevant urgent/pending actions and goals needing attention. The system handles prioritisation internally.

### CHECK
Answer: “How am I doing, and what needs attention?”
Return a short adaptive summary. If everything is fine, say so briefly. If something needs attention, explain the few most important issues. Do not dump every metric or goal.

### LOG
Answer: “What happened?”
Accept natural language. Interpret it into structured information, show the interpretation, optionally show relevant patterns/comparisons, and ask the user to Confirm or Edit. Save only after confirmation.

### MORE
A universal search/explore gateway, not a module drawer. It should answer questions about stored goals, logs, systems, patterns, preferences, and history.

## Pattern intelligence

For recurring behaviour, distinguish:
- Observed pattern
- Possible next pattern
- Conditions under which the pattern should be broken

Do not blindly extrapolate. State uncertainty. Avoid unsafe recommendations.

## Underlying model

Use a minimal connected Life Graph of goals, actions, logs/events, patterns, measurements, preferences, context, and relationships. This is an internal data model, not a complex UI.

Optional life dimensions are Fun, Mind, Career, Money, Body, People, Purpose, and Daily Life. They are lenses for interpretation/review, not mandatory categories.

## V0.1 boundaries

Build:
- Neutral gateway
- DO / CHECK / LOG / More
- Natural-language input
- Interpretation preview + Confirm/Edit
- Basic goals/actions/logs
- Simple explainable pattern detection
- Minimal prioritisation
- Local persistence
- Basic edit/delete
- Responsive UI

Do not build yet:
- Giant cockpit/dashboard
- Knowledge wiki or resource vault
- Complex habit screens
- Focus timer as the core workflow
- WhatsApp/Microsoft To Do integrations
- Elaborate dimensions UI
- Many settings
- Multi-user features

## Technical preference

Start with a simple single-page application, preferably one `index.html` with embedded HTML/CSS/JavaScript. Use browser `localStorage` for a local-first prototype. Avoid unnecessary dependencies. GitHub Pages is the deployment target.

An LLM integration is optional. If using an external model, never expose the API key in browser code. Use a secure backend/proxy. Clearly distinguish actual LLM capabilities from deterministic rule-based logic.

## How you should work

- Preserve the product philosophy above when making changes.
- Do not add features simply because they are common in productivity apps.
- Ask one essential clarification at a time when needed.
- Prefer the smallest useful implementation.
- Keep existing working behaviour intact when iterating.
- Explain trade-offs and identify what is implemented versus planned.
- After each major change, provide a concise test checklist.

First inspect the existing repository and identify what is implemented. Do not assume this specification means the feature already exists. Then recommend the smallest next step.
