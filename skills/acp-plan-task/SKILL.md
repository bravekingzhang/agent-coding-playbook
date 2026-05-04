---
name: acp-plan-task
description: Use when a request is large, ambiguous, or spans multiple files/components and the user has NOT yet approved an implementation approach. Produces a verifiable plan via Plan Mode and a TodoWrite breakdown, then hands off to a more specific skill (bug-fix, refactor, feature-add) for execution.
version: 1.0.0
---

# Plan Task Skill

Use this skill when the work is too big or too unclear to start coding directly.

The goal is not to write a plan for its own sake.

The goal is to produce the smallest plan that makes execution safe — clear scope, clear non-goals, clear verification, clear handoff.

---

## When to Use

Use this skill when ANY of these are true:

- The change spans more than 2–3 files and the touchpoints are not obvious.
- The request mixes multiple concerns (refactor + feature + bug fix).
- The success criteria are not yet defined.
- The user said "design" / "architect" / "figure out how to" rather than "do".
- You are about to enter a high-risk area (auth, payment, migration, public API).

If the task is small and obvious, skip this skill and go straight to `acp-bug-fix`, `acp-refactor`, or `acp-feature-add`.

---

## Workflow

### 1. Restate the Goal

In one or two sentences, write what success looks like from the user's perspective.

If you cannot do this, the task is not ready for planning — go back and ask the user.

---

### 2. Map the Surface Area

Use the **Explore subagent** to identify, without polluting the main session:

- Files and modules likely involved.
- Existing patterns the work should follow.
- Tests that already cover the affected behavior.
- Risks (high-risk modules, public APIs, data paths).

Quote file paths in the plan so reviewers can verify your reading is correct.

---

### 3. Decompose Into Verifiable Steps

Break the work into steps that each:

- Make a single conceptual change.
- End in a state where verification can run (tests pass, build succeeds).
- Can be reverted independently.

Bad: "rewrite the auth module".
Good: "1. add failing test for X; 2. extract helper Y; 3. swap implementation; 4. delete old path".

Record the steps in a TodoWrite list so progress is visible during execution.

---

### 4. Define Verification Up Front

For each step, write down how it will be verified:

- Which test file is updated or added.
- Which command is run (`pnpm test`, `cargo check`, ...).
- What manual reproduction would prove it.

A step without a verification path is not a step — it is a wish.

---

### 5. Use Plan Mode for Sign-Off

Present the plan via **ExitPlanMode** so the user can approve or push back before any code is written.

Do not start editing until the plan is approved.

---

### 6. Hand Off to an Execution Skill

Once approved:

- Bug fix → `acp-bug-fix` skill
- Behavior-preserving cleanup → `acp-refactor` skill
- New behavior → `acp-feature-add` skill
- Test-first change → `acp-test-first` skill

This skill ends at handoff.

---

## Output Format

```text
Goal:
- ...

Non-goals:
- ...

Affected files / modules:
- ...

Risks:
- ...

Steps:
1. <step> — verified by <how>
2. <step> — verified by <how>
3. ...

Handoff:
- This will be executed under the <skill-name> skill.
```

---

## Guardrails

Stop and ask the user before continuing if:

- The plan grows beyond what the user described.
- A step touches a high-risk area (auth, payment, migration, security, privacy, public API).
- You realize the request is actually two separate tasks. In that case, propose splitting them.
