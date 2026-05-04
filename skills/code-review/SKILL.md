# Code Review Skill

Use this skill when reviewing code written by humans or AI coding agents.

The goal is not to praise the implementation.

The goal is to find behavior changes, risks, missing verification, and unnecessary complexity.

---

## Review Mindset

Review the diff, not the summary.

An agent's explanation may be useful, but it is not evidence.

Evidence lives in:

- The diff.
- Tests.
- Build output.
- Runtime behavior.
- Logs.
- Product requirements.

---

## Review Workflow

### 1. Understand the Intended Change

Identify:

- What problem is this change trying to solve?
- What behavior should change?
- What behavior should remain unchanged?
- Which users or systems are affected?

If the intent is unclear, ask before approving.

---

### 2. Trace Every Meaningful Diff

For each meaningful changed block, ask:

> Why is this change necessary for the stated goal?

Flag changes that are:

- Unrelated to the task.
- Formatting-only noise.
- Accidental behavior changes.
- Opportunistic cleanup.
- Premature abstraction.

---

### 3. Check Behavior and Edge Cases

Look for:

- Null or empty values.
- Error handling.
- Retry behavior.
- Race conditions.
- Backward compatibility.
- Performance impact.
- Security impact.
- Data loss risk.

---

### 4. Check Verification

A PR is weaker if it has no verification evidence.

Look for:

- Unit tests.
- Integration tests.
- Type checks.
- Lint.
- Build results.
- Manual test notes.

If verification is missing, ask for it.

---

### 5. Decide Review Outcome

Use one of these outcomes:

- Approve: small change, clear intent, adequate verification.
- Comment: minor issues or questions.
- Request changes: behavior risk, missing verification, unrelated changes, or unclear intent.

---

## Output Format

```text
Summary:
- ...

Main risks:
- ...

Required changes:
- ...

Suggested improvements:
- ...

Verification gaps:
- ...
```

---

## AI-Generated Code Warning Signs

Be extra careful when the diff contains:

- Large unrelated rewrites.
- New abstractions for small tasks.
- Generic helper functions with only one caller.
- Renamed APIs without migration.
- Tests that only verify implementation details.
- Comments that describe obvious code.
- Confident summaries with no checks.
