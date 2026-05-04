# High-Risk Change Checklist

Use this checklist when an AI coding agent modifies sensitive or production-critical code.

---

## High-Risk Areas

A change is high-risk if it touches:

- [ ] Authentication.
- [ ] Authorization.
- [ ] Payment or billing.
- [ ] Data migration.
- [ ] Data deletion.
- [ ] Database schema.
- [ ] Security-sensitive code.
- [ ] Privacy-sensitive data.
- [ ] Public API behavior.
- [ ] Production release workflow.
- [ ] Large-scale refactoring.

---

## Required Review

- [ ] Human reviewer assigned.
- [ ] Diff reviewed line by line.
- [ ] Behavior change documented.
- [ ] Rollback plan documented.
- [ ] Monitoring or logs confirmed.
- [ ] Stakeholders informed if needed.

---

## Verification Evidence

- [ ] Unit tests.
- [ ] Integration tests.
- [ ] E2E tests.
- [ ] Type checks.
- [ ] Lint.
- [ ] Build.
- [ ] Manual test notes.
- [ ] Gray release result if applicable.

---

## Decision

Choose one:

- [ ] Go.
- [ ] Go with caution.
- [ ] No-go.

Reason:

```text
...
```

---

## Rule

AI-generated summaries are not enough for high-risk changes.

Read the diff.
