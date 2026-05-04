# Refactor Skill

Use this skill when the user asks for refactoring, cleanup, simplification, modularization, or architecture improvement.

The goal of refactoring is to improve structure while preserving behavior.

If behavior changes, it is not just refactoring anymore.

---

## Refactor Rules

### 1. Define the Refactor Goal

Before editing, state the exact goal:

- Reduce duplication.
- Improve naming.
- Extract a function.
- Split a large module.
- Remove dead code.
- Improve testability.
- Simplify control flow.

Do not refactor just because code looks old or ugly.

---

### 2. Preserve Behavior

Public behavior must remain unchanged unless the user explicitly asks for a behavior change.

Before editing, identify:

- Public APIs.
- Input/output behavior.
- Existing tests.
- Compatibility requirements.
- Known edge cases.

---

### 3. Refactor in Small Steps

Prefer small, reversible changes.

Good steps:

- Rename one concept.
- Extract one function.
- Move one helper.
- Remove one duplication.
- Add one missing test before restructuring.

Bad steps:

- Rewrite the whole module.
- Change naming, structure, and behavior together.
- Introduce a framework.
- Split files without clear boundaries.

---

### 4. Run Checks Frequently

After each meaningful step, run relevant checks when possible:

- Existing tests.
- Type checks.
- Lint.
- Build.

If checks are unavailable, explain the risk.

---

## Output Format

```text
Refactor goal:
- ...

Behavior preserved:
- ...

Changed:
- ...

Verified:
- ...

Risk:
- ...
```

---

## Stop Conditions

Stop and ask for confirmation if:

- The refactor requires public API changes.
- The change touches high-risk modules.
- The diff becomes larger than expected.
- You discover the code needs redesign rather than refactor.
