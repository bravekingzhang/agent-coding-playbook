# PR Review Checklist

Use this checklist when reviewing a pull request created by a human or an AI coding agent.

---

## Intent

- [ ] Is the purpose of the PR clear?
- [ ] Is the change scope clear?
- [ ] Is the PR solving one problem, not several unrelated problems?
- [ ] Are non-goals documented?

---

## Diff

- [ ] Is the diff reasonably small?
- [ ] Are unrelated files untouched?
- [ ] Are formatting-only changes avoided?
- [ ] Are public APIs unchanged unless explicitly required?
- [ ] Are new dependencies justified?

---

## Implementation

- [ ] Is the solution simple enough?
- [ ] Is there unnecessary abstraction?
- [ ] Is error handling appropriate?
- [ ] Are edge cases covered?
- [ ] Is backward compatibility considered?

---

## Tests and Checks

- [ ] Unit tests added or updated if needed.
- [ ] Existing tests pass.
- [ ] Type checks pass.
- [ ] Lint passes.
- [ ] Build passes.
- [ ] Manual verification is documented if needed.

---

## Risk

- [ ] Does this touch high-risk areas?
- [ ] Is rollback possible?
- [ ] Is monitoring/logging sufficient?
- [ ] Does this require additional reviewers?

---

## AI-Specific Review

- [ ] Did the agent over-expand the task?
- [ ] Did the agent invent requirements?
- [ ] Did the agent introduce generic utilities with only one caller?
- [ ] Did the agent claim checks passed without evidence?
- [ ] Did the agent hide uncertainty in a confident summary?

---

## Review Outcome

Choose one:

- [ ] Approve.
- [ ] Comment.
- [ ] Request changes.

Reason:

```text
...
```
