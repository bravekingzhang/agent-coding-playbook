# Bad Prompts

Bad prompts often make AI coding agents guess.

Guessing leads to broad diffs, accidental behavior changes, and fake confidence.

---

## Bad Prompt 1

```text
Fix this bug.
```

Why it is bad:

- No current behavior.
- No expected behavior.
- No reproduction.
- No scope.
- No verification.

Better:

```text
Fix the crash when the profile page renders a user without an avatar. Show the default avatar. Do not change the user API. Add or update a regression test if possible.
```

---

## Bad Prompt 2

```text
Make this code better.
```

Why it is bad:

- “Better” is undefined.
- Agent may rewrite unrelated code.
- Agent may introduce unnecessary abstraction.
- No way to know when the task is complete.

Better:

```text
Reduce duplication in the validation logic while preserving behavior and public API. Keep the diff small. Run related tests.
```

---

## Bad Prompt 3

```text
Optimize performance.
```

Why it is bad:

- No metric.
- No baseline.
- No target.
- No affected path.
- No verification method.

Better:

```text
Investigate why the dashboard takes more than 3 seconds to render with 1,000 rows. Identify the bottleneck first. Do not change behavior until the bottleneck is explained. Propose the smallest fix and state how to measure improvement.
```

---

## Bad Prompt 4

```text
Refactor this whole directory.
```

Why it is bad:

- Too broad.
- Hard to review.
- High chance of behavior changes.
- Hard to roll back.

Better:

```text
Refactor only the duplicated date formatting helpers in this directory. Preserve all existing output formats. Do not move unrelated files. Run related tests.
```

---

## Rule

If a prompt does not define goal, scope, and verification, the agent will define them for you.

That is usually where trouble starts.
