# Vibe Coding Risk Level

Vibe coding is not always bad.

The problem is using vibe coding in places where the risk is too high.

This document defines a simple risk model.

---

## Level 1: Low Risk

Examples:

- Personal scripts.
- Throwaway prototypes.
- Internal demos.
- One-off data formatting.
- UI mockups.
- Learning exercises.

Suggested mode:

```text
Vibe coding is acceptable.
Automated checks are still preferred.
Human review is optional.
```

---

## Level 2: Medium Risk

Examples:

- Normal business features.
- UI behavior changes.
- Non-critical backend logic.
- Internal tools used by a team.
- Refactors with good test coverage.

Suggested mode:

```text
AI-generated code is acceptable.
Automated checks are required.
Human review is recommended.
```

---

## Level 3: High Risk

Examples:

- Authentication.
- Authorization.
- Payment.
- Billing.
- Data migration.
- Data deletion.
- Security-sensitive logic.
- Privacy-sensitive data.
- Production release workflows.
- Public API changes.
- Large refactors.

Suggested mode:

```text
AI can assist.
Automated checks are required.
Human review is mandatory.
Rollback planning is required.
```

---

## Rule of Thumb

The higher the cost of a mistake, the less you should rely on vibe coding.

Do not ask:

> Can AI write this?

Ask:

> What happens if AI writes this wrong?

---

## Review Policy

| Risk Level | AI Coding | Automated Checks | Human Review | Rollback Plan |
| --- | --- | --- | --- | --- |
| Low | Yes | Recommended | Optional | Optional |
| Medium | Yes | Required | Recommended | Optional |
| High | Assist only | Required | Mandatory | Required |
