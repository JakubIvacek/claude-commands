---
description: "Refactor described code without intentionally changing behavior — identify existing invariants first, change incrementally, verify with tests."
argument-hint: "<what to refactor>"
---

Refactor this: $ARGUMENTS

This is a behavior-preserving refactor, not a rewrite — the observable behavior before and after must match. Follow these steps:

1. **Identify the existing invariants.** Read the code being refactored and its callers/tests to understand what it must still do afterward: inputs/outputs, side effects, error behavior, edge cases already relied upon elsewhere.

2. **Establish a green baseline.** Run the relevant existing tests before touching anything. If there's no test coverage for this code, note that — a refactor without any safety net is riskier, so be more conservative about scope.

3. **Make the change incrementally.** Prefer a sequence of small, individually-verifiable steps (extract a function, rename, inline, restructure) over one large rewrite. After each step, re-run the tests before moving to the next.

4. **Don't change behavior along the way.** No fixing bugs you notice, no adding features, no altering public signatures unless that's explicitly part of the ask — note anything else you spot instead of touching it here.

5. **Verify the result.** Run the full relevant test suite (and typecheck/build if applicable) and confirm it's still green. If tests were missing for the refactored area, that's expected to stay true — this command doesn't add test coverage (`/test` does).

6. **Summarize** what changed structurally, confirm behavior is unchanged, and flag anything you deliberately left alone.
