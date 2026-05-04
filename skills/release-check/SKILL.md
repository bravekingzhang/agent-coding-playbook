# Release Check Skill

Use this skill before releasing, deploying, publishing, or merging a change into a production-bound branch.

The goal is to reduce release risk, not to create a long ceremony.

---

## Release Review Workflow

### 1. Identify the Release Scope

Summarize:

- What is being released?
- Which features, fixes, or refactors are included?
- Which platforms, services, or users are affected?
- Is this a full release, gray release, hotfix, rollback, or experiment?

---

### 2. Classify Risk

Classify the release as low, medium, or high risk.

High-risk signals:

- Auth or permission logic.
- Payment or billing logic.
- Data migration.
- Database schema changes.
- Security-sensitive code.
- Privacy-sensitive data.
- Public API changes.
- Large refactors.
- Weak test coverage.
- Tight deadline or emergency release.

---

### 3. Check Verification Evidence

Look for:

- Unit tests.
- Integration tests.
- E2E tests.
- Type checks.
- Lint.
- Build artifacts.
- Manual verification notes.
- Gray release observations.
- Rollback rehearsal or rollback plan.

If evidence is missing, mark it as a release risk.

---

### 4. Check Operational Readiness

Confirm:

- Monitoring exists.
- Logs are available.
- Alerts are configured if needed.
- Rollback path is clear.
- Owners are known.
- Stakeholders are informed.
- User-facing impact is understood.

---

## Output Format

```text
Release scope:
- ...

Risk level:
- Low / Medium / High

Verification evidence:
- ...

Missing evidence:
- ...

Rollback plan:
- ...

Recommendation:
- Go / Go with caution / No-go
```

---

## Rule

Do not say a release is safe only because the code compiles.

A release is safe when the change scope, verification evidence, runtime observability, and rollback path are all clear.
