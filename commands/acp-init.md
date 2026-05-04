---
name: acp-init
description: Initialize the Agent Coding Playbook in the current project. Writes a CLAUDE.md (and optionally AGENTS.md) at the project root using the playbook's baseline rules, with placeholders for tech stack, build/test/lint commands, and high-risk areas.
---

# /acp-init

You are setting up the Agent Coding Playbook in the user's current project.

## What this command does

Create (or refuse to overwrite) the following at the project root:

1. `CLAUDE.md` — baseline behavior rules for Claude Code, with project-specific placeholders.
2. (Optional) `AGENTS.md` — equivalent rules for Codex / Cursor / other agents, only if the user asks for it.

## Steps

1. **Detect existing files.** Use `Read` to check whether `CLAUDE.md` and `AGENTS.md` already exist at the project root.

   - If `CLAUDE.md` exists, do NOT overwrite. Show its first lines and ask the user whether to:
     - skip,
     - append a "Playbook section" at the end, or
     - back up the existing file (`CLAUDE.md.bak`) and replace it.

2. **Detect project context (best effort, do not block on this).** Quickly look for signals so the placeholders can be pre-filled:

   - `package.json` → likely Node/TS, scripts for `test` / `lint` / `build` / `typecheck`.
   - `pyproject.toml` / `requirements.txt` → Python.
   - `Cargo.toml` → Rust.
   - `go.mod` → Go.
   - `pnpm-lock.yaml` / `yarn.lock` / `package-lock.json` → package manager.

   If detection is unclear, leave the placeholder as `...` and tell the user which fields still need to be filled.

3. **Write `CLAUDE.md`** using the content below as the template. Replace `{{tech_stack}}`, `{{install_cmd}}`, `{{test_cmd}}`, `{{typecheck_cmd}}`, `{{lint_cmd}}`, `{{build_cmd}}`, and `{{high_risk_areas}}` with detected or `...` values.

4. **Report back** to the user with:
   - The file(s) created.
   - Any placeholder still set to `...`.
   - A one-line suggestion: "Open CLAUDE.md and fill the remaining placeholders before your next agent session."

## CLAUDE.md template to write

````markdown
# CLAUDE.md

This file defines the coding behavior expected from Claude when working in this repository.

The goal is not to produce more code.

The goal is to produce the smallest correct change that satisfies the user's request and can be verified.

---

## Project Context

Tech stack:

```text
{{tech_stack}}
```

Common commands:

```bash
# install
{{install_cmd}}

# test
{{test_cmd}}

# typecheck
{{typecheck_cmd}}

# lint
{{lint_cmd}}

# build
{{build_cmd}}
```

---

## 1. Think Before Coding

Before editing code, explain briefly:

- What you think the user is asking for.
- Which files or modules are likely involved.
- What assumptions you are making.
- What risks or ambiguities exist.

If the request is ambiguous, ask for clarification before making changes. Do not silently guess important requirements.

---

## 2. Simplicity First

Prefer the simplest solution that solves the current problem. Do not add abstractions unless they are clearly required by the current task.

Avoid: new frameworks, new layers, new generic utilities, premature configuration, "future-proof" designs that are not needed now.

A small direct fix is usually better than a clever generalized design.

---

## 3. Surgical Changes Only

Only modify files that are necessary for the task. Every changed line should be traceable to the user's request.

Do not rewrite unrelated code, reformat unrelated files, rename existing APIs unless explicitly asked, clean up old code you did not touch, or change behavior outside the requested scope.

If you discover unrelated problems, report them separately instead of fixing them silently.

---

## 4. Goal-Driven Execution

Turn the user's request into verifiable goals. Whenever possible:

- Write or identify a failing test first.
- Make the smallest change to pass the test.
- Run relevant checks.
- Report what was verified.

Do not claim success without verification.

---

## 5. Context Discipline

Do not load unnecessary files. Prefer reading the smallest set of files needed to understand the task. When the task becomes too large, suggest splitting it into smaller steps.

---

## 6. Human Review Awareness

Your summary is not a substitute for human review. For high-risk changes, explicitly warn the user.

High-risk areas in this project:

```text
{{high_risk_areas}}
```

Generic high-risk categories: authentication, authorization, payment, data migration, security, privacy, production release, public API behavior, large refactors.

---

## 7. Communication Style

Be concise, concrete, and honest. Do not hide uncertainty. Do not say the task is complete if verification was not performed.

End every task with:

```text
Changed:
- ...

Verified:
- ...

Not verified:
- ...

Risks:
- ...
```
````

## AGENTS.md (only if user asks)

If the user explicitly asks for `AGENTS.md` as well, write a parallel file with the same principles in a tool-neutral voice. Otherwise do not create it.

## Final note

After writing, remind the user that the playbook also ships skills (`acp-bug-fix`, `acp-code-review`, `acp-refactor`, `acp-release-check`, `acp-test-first`, `acp-feature-add`, `acp-investigate`, `acp-plan-task`). They will be invoked automatically when the user's request matches their description.
