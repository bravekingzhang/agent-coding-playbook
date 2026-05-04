---
name: acp-feature-add
description: Use when the user asks to add a new feature, add a new API/endpoint/page/component, implement a new capability, or extend existing functionality with new behavior. Forces a plan-before-code loop, scoping non-goals, and verifying the new behavior end-to-end.
version: 1.0.0
---

# Feature Add Skill

Use this skill when the user asks to build something new — a feature, endpoint, page, component, or capability.

The goal is not to start typing as fast as possible.

The goal is to clarify the contract, plan the smallest viable implementation, and verify the new behavior actually works before claiming done.

---

## Workflow

### 1. Clarify the Contract

Before writing code, write down:

- What is the new behavior?
- What is the input?
- What is the output, side effect, or state change?
- Who calls this? Who is affected by it?
- What is explicitly out of scope (non-goals)?
- What existing behavior must remain unchanged?

If any of these are unclear, ask. Do not invent requirements.

---

### 2. Plan Before Coding

For anything beyond a trivial 1-file change, enter **Plan Mode** (ExitPlanMode) before editing.

A good plan answers:

- Which files will be created or modified?
- What is the minimum set of changes that satisfies the contract?
- Are there existing patterns in the codebase to follow? Use the Explore subagent to find them rather than inventing new patterns.
- What is the verification strategy?

Get the plan approved before writing code.

For multi-step features, also create a TodoWrite list so progress is visible and each step ends in a verifiable state.

---

### 3. Reuse Before Creating

Before adding a new abstraction:

- Search the codebase for an existing utility, component, or pattern that already solves part of the problem.
- Prefer extending an existing thing over creating a new generic one.
- Do not introduce a new dependency unless the alternative is clearly worse.

A new generic helper with one caller is a smell, not a feature.

---

### 4. Implement the Smallest Viable Version

Build the smallest version that satisfies the contract.

Do not:

- Add configuration options that no one asked for.
- Add fields that "might be useful later".
- Add abstractions for hypothetical second callers.
- Wrap existing libraries unless there is a concrete reason.

If you find yourself wanting to generalize, stop and finish the concrete case first.

---

### 5. Verify End-to-End

A new feature is not done when the file compiles.

Run, in order of preference:

- A test that exercises the new behavior (write one if the project supports tests).
- The relevant typecheck, lint, and build commands.
- A manual reproduction of the user-facing path.

If verification cannot be run in the current environment, say so explicitly.

---

## Output Format

```text
Contract:
- ...

Plan:
- ...

Changed:
- ...

Verified:
- ...

Not verified:
- ...

Risks:
- ...
```

---

## Guardrails

Stop and ask for confirmation if:

- The feature touches auth, permission, payment, data migration, security, privacy, public API, or release workflow.
- The feature requires changing a public API or breaking backward compatibility.
- The plan grows beyond the user's stated scope.
- The implementation requires a new framework or major dependency.
