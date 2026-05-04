# Before Coding Checklist

Use this checklist before asking an AI coding agent to modify code.

---

## Task Understanding

- [ ] Is the user request clear?
- [ ] Is the expected behavior clear?
- [ ] Is the current behavior clear?
- [ ] Are important constraints written down?
- [ ] Are non-goals written down?

---

## Scope

- [ ] Which files or modules are likely involved?
- [ ] Which files or modules should not be touched?
- [ ] Is this a small fix, feature change, refactor, or release task?
- [ ] Is the expected diff size reasonable?

---

## Risk

- [ ] Does this touch auth, permission, payment, data, security, privacy, release, or public API logic?
- [ ] Does this require human review?
- [ ] Does this require rollback planning?

---

## Verification

- [ ] Is there an existing test?
- [ ] Should a failing test be added first?
- [ ] What checks should run after the change?
- [ ] What manual verification is needed?

---

## Good Prompt Shape

A good coding-agent task should include:

```text
Goal:
- ...

Context:
- ...

Scope:
- ...

Do not change:
- ...

Verification:
- ...

Risk:
- ...
```
