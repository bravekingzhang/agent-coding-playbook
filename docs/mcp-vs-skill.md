# MCP vs Skill

MCP and Skill are often mentioned together, but they are not the same thing.

A simple way to remember:

> MCP gives the agent hands. Skill teaches the agent how to work.

---

## What Is MCP?

MCP, or Model Context Protocol, is a way to connect AI agents with external tools and systems.

Through MCP, an agent may access capabilities such as:

- Reading files.
- Searching documentation.
- Querying databases.
- Calling APIs.
- Reading GitHub issues.
- Opening browser pages.
- Sending notifications.

MCP is about tool access.

---

## What Is a Skill?

A Skill is a reusable task guide.

It tells the agent how to perform a specific kind of work.

A Skill may include:

- Workflow steps.
- Rules.
- Examples.
- Checklists.
- Output format.
- Risk guardrails.

Skill is about work method.

---

## Example: Release Work

For a release task, MCP tools may allow the agent to:

- Read CI status.
- Check GitHub pull requests.
- Fetch build artifacts.
- Send a message to a chat system.

But the release Skill tells the agent:

- What to check before release.
- How to classify risk.
- When to stop and ask for approval.
- What rollback information is required.
- How to summarize release readiness.

Without MCP, the agent has no hands.

Without Skill, the agent has no discipline.

---

## Design Rule

Do not use MCP as a replacement for process.

Do not use Skill as a replacement for tools.

Use them together:

```text
Skill = workflow + judgment + guardrails
MCP = tool access + external actions
Agent = reasoning + execution loop
```

---

## Enterprise Pattern

For enterprise teams, a useful pattern is:

```text
Business workflow → Skill
Business system access → MCP
Risk control → Checklist
Final decision → Human review when needed
```

This keeps AI coding agents useful without giving them unlimited freedom.
