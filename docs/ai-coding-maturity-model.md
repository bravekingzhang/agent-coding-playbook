# AI Coding Maturity Model

This model helps teams understand how mature their AI coding practice is.

It is not a ranking of tools or models.

It is a way to evaluate whether a team has turned AI coding from individual experimentation into repeatable engineering practice.

---

## Level 0: Ad Hoc Usage

AI coding is used casually by individuals.

Typical signs:

- No shared rules.
- No project-level `CLAUDE.md` or `AGENTS.md`.
- No shared prompts or skills.
- No review policy for AI-generated code.
- Success depends on individual experience.

Main risk:

> AI coding output is inconsistent and hard to trust.

---

## Level 1: Shared Rules

The team has basic rules for AI coding agents.

Typical signs:

- Project-level agent instructions exist.
- The team agrees on minimal-change principles.
- High-risk areas are documented.
- Developers know that agent summaries are not a substitute for diff review.

Main improvement:

> Agents start following team expectations instead of acting like generic code generators.

---

## Level 2: Task Skills

The team has reusable skills for common tasks.

Typical signs:

- Bug fix skill.
- Code review skill.
- Refactor skill.
- Release check skill.
- Test-first skill.
- Reusable output formats.

Main improvement:

> Team experience becomes reusable instead of staying in individual heads.

---

## Level 3: Verification Loop

The team connects AI coding work with automated checks.

Typical signs:

- Tests, typecheck, lint, and build commands are documented.
- Agents are expected to run checks.
- Missing verification must be reported.
- PR templates include AI-specific review items.

Main improvement:

> AI coding becomes evidence-driven instead of summary-driven.

---

## Level 4: Tool and Workflow Integration

The team integrates tools, MCP servers, CI, issue systems, and documentation sources.

Typical signs:

- Agents can read relevant docs and issue context.
- MCP tools are scoped by task.
- Release checks can read CI and deployment status.
- Review agents can inspect diffs and test output.
- Sensitive tools require human confirmation.

Main improvement:

> Agents can participate in real engineering workflows without unlimited permissions.

---

## Level 5: Managed Engineering System

AI coding is part of the team's engineering management system.

Typical signs:

- AI coding rules are versioned.
- Skills are maintained like engineering assets.
- Risk levels are defined.
- Review policies are enforced.
- Metrics are tracked, such as defect rate, review time, test coverage, rollback rate, and cycle time.

Main improvement:

> AI coding becomes a governed engineering capability, not a personal productivity trick.

---

## Summary

```text
L0: Ad hoc usage
L1: Shared rules
L2: Task skills
L3: Verification loop
L4: Tool and workflow integration
L5: Managed engineering system
```

The goal is not to reach the highest level immediately.

The goal is to avoid pretending that casual AI coding is already engineering practice.
