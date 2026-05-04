---
name: acp-investigate
description: Use when the user asks to understand, explain, trace, audit, or explore code WITHOUT modifying it. Examples — "how does X work", "where is Y called", "why does this branch exist", "trace the request flow". Stays read-only and does not produce a fix.
version: 1.0.0
---

# Investigate Skill

Use this skill when the user wants to understand code, not change it.

The goal is not to fix a problem.

The goal is to produce an accurate, evidence-based explanation of what the code does, where it lives, and why.

If the user is asking a question rather than asking for a change, stay in this skill until they explicitly ask for a code change.

---

## Mode: Read-Only

While in this skill:

- Do not modify any source file.
- Do not "fix" code you find suspicious — report it instead.
- Do not run write-side tools (commits, branch creation, deploys).
- Reading files, running tests, and grepping the repo are all fine.

If you discover a bug or unrelated issue during investigation, surface it in the report. Do not silently patch it.

---

## Workflow

### 1. Restate the Question

Before searching, write down:

- What does the user want to know?
- What kind of answer would satisfy them — a file path, a sequence diagram, a list of call sites, a behavioral explanation?
- What is out of scope?

A vague question produces a vague answer. Ask for clarification if the question is ambiguous.

---

### 2. Delegate Search to a Subagent

For anything beyond a single grep, prefer the **Explore subagent** over loading files into the main session.

Explore is faster, cheaper, and keeps the main context clean. Reserve direct file reads for the small set of files you actually need to quote.

Good queries to delegate:

- "Find every call site of `renderAvatar` and group by file."
- "Locate the entry point that handles `/api/orders` and trace the next 2 layers of calls."
- "Find every place that reads `process.env.STRIPE_KEY`."

---

### 3. Read Only What You Need

For the small set of files you do read directly:

- Read the specific functions or sections, not the whole file when avoidable.
- Quote line numbers when explaining.
- If a file is too large, read targeted ranges.

---

### 4. Build the Explanation From Evidence

Every claim in the report should be backed by:

- A file path and line range, or
- A test or runtime observation, or
- A clearly labeled inference ("this is my interpretation, not directly stated").

Do not paraphrase code into a confident summary that the code does not actually support.

---

### 5. Report

Produce a structured answer. Keep it as short as the question allows.

---

## Output Format

```text
Question:
- ...

Answer:
- ...

Evidence:
- file:line — what it shows
- file:line — what it shows

Open questions:
- ...

Things noticed (not fixed):
- ...
```

---

## Exit Condition

If the user, after seeing the investigation, asks for a fix or change, exit this skill and switch to the appropriate one (`acp-bug-fix`, `acp-refactor`, `acp-feature-add`).

Do not start editing while still in investigate mode.
