# Bug Fix Skill

Use this skill when the user asks you to fix a bug, investigate an error, or explain why something is failing.

The goal is not to guess the cause quickly.

The goal is to reproduce, isolate, fix, and verify.

---

## Workflow

### 1. Understand the Bug

Before changing code, identify:

- What is the observed behavior?
- What is the expected behavior?
- When did it start happening?
- Is there an error message, log, stack trace, screenshot, or failing test?
- Which users, environments, platforms, or versions are affected?

If the bug report is vague, ask for the missing reproduction details.

---

### 2. Reproduce First

Do not fix a bug that has not been reproduced or clearly reasoned about.

Prefer one of these reproduction forms:

- A failing unit test.
- A failing integration test.
- A minimal manual reproduction.
- A log or stack trace that points to the failing path.

If reproduction is impossible in the current environment, state that clearly.

---

### 3. Isolate the Root Cause

Before editing, explain the likely root cause.

Good root cause statements look like:

```text
The crash happens because `user.profile` can be null, but `renderAvatar` reads `user.profile.avatarUrl` without a null check.
```

Bad root cause statements look like:

```text
This is probably a state issue.
```

Be specific.

---

### 4. Make the Smallest Fix

Fix the bug with the smallest safe change.

Do not:

- Rewrite the whole module.
- Rename unrelated variables.
- Reformat unrelated files.
- Add new abstractions unless necessary.
- Fix nearby issues unless they are part of the same bug.

Every changed line must be related to the bug.

---

### 5. Verify the Fix

Run the most relevant checks available:

- The failing test.
- Related unit tests.
- Type check.
- Lint.
- Build.
- Manual reproduction steps.

If checks cannot be run, explain why.

---

## Output Format

At the end, summarize:

```text
Root cause:
- ...

Changed:
- ...

Verified:
- ...

Not verified:
- ...

Risk:
- ...
```

---

## Guardrails

Stop and ask for human confirmation if the bug fix touches:

- Auth or permission logic.
- Payment logic.
- Data migration.
- Security-sensitive code.
- Public API behavior.
- Large-scale refactoring.
