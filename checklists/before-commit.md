# Before Commit Checklist

Use this checklist before committing code generated or modified by an AI coding agent.

---

## Diff Discipline

- [ ] Did the agent modify only necessary files?
- [ ] Is every changed line related to the task?
- [ ] Are there unrelated formatting changes?
- [ ] Are there opportunistic cleanups that should be reverted?
- [ ] Did the agent introduce new abstractions without need?

---

## Behavior

- [ ] Is the intended behavior change clear?
- [ ] Are unintended behavior changes avoided?
- [ ] Are edge cases handled?
- [ ] Is backward compatibility preserved when needed?

---

## Verification

- [ ] Tests passed.
- [ ] Type checks passed.
- [ ] Lint passed.
- [ ] Build passed.
- [ ] Manual verification completed if needed.

If any check was not run, document why.

---

## Human Review

- [ ] Does this change require human review?
- [ ] Are high-risk areas touched?
- [ ] Are risks clearly documented in the commit or PR?

---

## Commit Message

A good commit message should explain the actual change, not just mention AI.

Bad:

```text
update code
```

Good:

```text
fix: handle null profile avatar in user card
```
