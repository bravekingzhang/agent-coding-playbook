---
name: acp-test-first
description: Use when the user asks to fix a bug, add behavior, or change behavior in a project that has a test framework, AND the change can be expressed as an observable input/output contract. Writes a failing test first, then makes the smallest change to pass it.
version: 1.0.0
---

# Test First Skill

Use this skill when the user asks to fix a bug, add behavior, or make a change that can be verified through tests.

The goal is to let tests describe the expected behavior before implementation details are changed.

---

## When to Use

Use this skill for:

- Bug fixes.
- Behavior changes.
- Edge case handling.
- Regression prevention.
- Refactors that need safety coverage.

Do not force test-first work when the project has no test framework or when the task is purely exploratory. In that case, document the missing test environment.

---

## Workflow

### 1. Define Expected Behavior

Before writing code, write down:

- What should happen?
- What currently happens?
- What input triggers the behavior?
- What output, state, or side effect should be observed?

---

### 2. Write or Identify a Failing Test

Prefer a test that fails for the right reason.

A good failing test is:

- Focused.
- Easy to understand.
- Related to the user request.
- Not coupled to unnecessary implementation details.

Avoid tests that only verify that a mocked internal function was called unless that is the actual contract.

---

### 3. Make the Smallest Implementation Change

Change only the code needed to make the test pass.

Do not:

- Rewrite nearby code.
- Add generic abstractions.
- Change public APIs unless required.
- Add unrelated test cases in the same step.

---

### 4. Run the Test Again

After implementation:

- Run the new or changed test.
- Run related tests.
- Run typecheck, lint, or build if available.

If checks cannot be run, say so clearly.

---

## Output Format

```text
Expected behavior:
- ...

Failing test:
- ...

Implementation:
- ...

Verified:
- ...

Not verified:
- ...
```

---

## Guardrail

Do not change the test just to match a wrong implementation.

If the test reveals that the requirement is ambiguous or wrong, stop and ask for clarification.
