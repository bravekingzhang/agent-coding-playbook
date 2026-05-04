# MCP Tooling Guidelines

MCP tools can make AI coding agents more useful, but they also expand what agents can access and change.

The goal is not to connect every possible tool.

The goal is to expose the minimum useful toolset with clear boundaries.

---

## Principle 1: Tools Should Match Tasks

Do not give every agent every tool.

A bug-fix agent may need:

- File read access.
- Test execution.
- Log search.
- Git diff inspection.

A release-check agent may need:

- CI status.
- Artifact status.
- Deployment status.
- Rollback documentation.

A code-review agent may need:

- Pull request diff.
- Test results.
- Related issue context.

Tool access should follow the task.

---

## Principle 2: Prefer Read-Only First

Start with read-only tools whenever possible.

Read-only tools are safer for:

- Documentation lookup.
- Issue inspection.
- CI status checks.
- Log analysis.
- Pull request review.

Write tools should require stronger guardrails.

---

## Principle 3: Human Confirmation for High-Risk Actions

Require human confirmation for actions such as:

- Deploying to production.
- Deleting data.
- Modifying permissions.
- Rotating secrets.
- Merging high-risk pull requests.
- Sending external notifications.
- Changing database schema.

The agent can prepare the action.

The human should approve the action.

---

## Principle 4: Make Tool Results Auditable

When an agent uses a tool, the final report should include:

- Which tool was used.
- What was checked.
- What result was observed.
- What decision was made from that result.

Avoid hidden tool usage that cannot be reviewed later.

---

## Principle 5: Keep Tool Output Focused

Large tool outputs can pollute context.

Prefer tools that return:

- Relevant snippets.
- Structured summaries.
- Filtered logs.
- Specific status fields.

Avoid dumping huge logs or entire repositories into the session.

---

## Suggested Tool Tiers

### Tier 1: Safe Read Tools

- Read files.
- Search code.
- Read docs.
- Read issues.
- Read PR diffs.
- Read CI status.

### Tier 2: Local Execution Tools

- Run tests.
- Run typecheck.
- Run lint.
- Run build.

### Tier 3: Controlled Write Tools

- Create branch.
- Create commit.
- Open pull request.
- Add review comment.

### Tier 4: High-Risk Write Tools

- Merge pull request.
- Deploy.
- Rollback.
- Modify secrets.
- Modify production data.

Tier 4 tools should require human confirmation.

---

## Rule of Thumb

Do not ask:

> Can this tool make the agent more powerful?

Ask:

> Can this tool make the agent safer, more verifiable, or more useful for this task?
