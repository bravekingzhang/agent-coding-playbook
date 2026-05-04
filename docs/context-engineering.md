# Context Engineering

Context engineering is the practice of giving an AI coding agent the right information at the right time.

It is not about putting everything into the prompt.

It is about controlling signal and noise.

---

## Why Context Matters

AI coding agents do not understand a repository the way a senior engineer does.

They work from the context available in the current session:

- User messages.
- System instructions.
- Project rules.
- Files read by the agent.
- Tool results.
- Prior conversation.

If the context is too small, the agent guesses.

If the context is too large, important details get buried.

---

## Common Context Mistakes

### 1. Giving Too Little Context

Bad:

```text
Fix this bug.
```

Better:

```text
Fix the crash when the user opens the profile page without an avatar. The expected behavior is to show the default avatar. Do not change the profile API.
```

---

### 2. Giving Too Much Context

Bad:

```text
Here are all product docs, all APIs, all coding standards, and all meeting notes. Now fix one small UI bug.
```

Too much context creates noise.

The agent may attend to irrelevant details and miss the actual task.

---

### 3. Putting Everything in AGENTS.md

`AGENTS.md` should contain durable project-level behavior rules.

It should not contain every workflow, every API document, every edge case, or every historical decision.

Use Skills and docs for task-specific context.

---

## Recommended Layers

```text
Always loaded:
- CLAUDE.md / AGENTS.md
- Short project rules

Loaded when relevant:
- Skills
- Checklists
- API docs
- Architecture notes

Loaded on demand:
- Source files
- Logs
- Test output
- Runtime traces
```

---

## Practical Rule

Before giving context to an agent, ask:

> Does this information help complete the current task?

If not, keep it out of the session.

---

## Good Context Package

A good task context usually includes:

```text
Goal:
- What should be achieved?

Current behavior:
- What happens now?

Expected behavior:
- What should happen?

Scope:
- What can be changed?

Non-goals:
- What should not be changed?

Verification:
- How do we know it works?
```
