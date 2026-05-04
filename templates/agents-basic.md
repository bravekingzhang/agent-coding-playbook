# AGENTS.md Basic Template

Copy this file to the root of your project as `AGENTS.md`.

---

## Project

Name:

```text
...
```

Tech stack:

```text
...
```

Important directories:

```text
...
```

---

## Commands

```bash
# test
...

# typecheck
...

# lint
...

# build
...
```

---

## Rules for Coding Agents

- Understand the task before editing.
- Ask when requirements are ambiguous.
- Prefer minimal, direct changes.
- Avoid unrelated refactoring.
- Do not reformat unrelated files.
- Do not introduce dependencies without need.
- Keep every diff traceable to the request.
- Run relevant checks when possible.
- Report verification honestly.

---

## Human Review Required

Human review is required for:

- ...

---

## Done Means Verified

A task is not done because the agent says it is done.

A task is done when there is evidence:

- Tests pass.
- Type checks pass.
- Lint passes.
- Build succeeds.
- Manual verification is documented.
