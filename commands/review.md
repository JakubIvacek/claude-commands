---
description: "Review the current branch or working-tree changes for bugs, regressions, edge cases, missing tests, and maintainability issues. Reports findings only — changes nothing."
argument-hint: "[target-branch] (default: main)"
---

Review this diff: $ARGUMENTS

This is a report-only review: you never edit code, add tests, or fix anything here — that's `/fix` or `/implementation`'s job. Follow these steps:

1. **Determine the diff.** If a target branch is given in `$ARGUMENTS`, use it; otherwise default to the repo's main branch (check `main`/`master`, or the default branch via `gh repo view --json defaultBranchRef` if unsure). Diff the current branch against it with `git diff <target>...HEAD`. If there are also uncommitted working-tree changes, include those too and say so in the report.

2. **Read changed files in full**, not just the diff hunks — you need surrounding context to judge correctness, not just what moved.

3. **Look for**:
   - **Bugs and regressions** — logic errors, off-by-ones, null/undefined handling, broken existing behavior
   - **Edge cases** — empty inputs, boundary values, concurrent access, error paths left unhandled
   - **Missing tests** — new logic or bug fixes with no corresponding test coverage
   - **Maintainability** — dead code, unclear naming, duplicated logic, functions/files that grew too large

4. **Assign severity** to each finding: CRITICAL (breaks or regresses behavior / security risk), HIGH (real bug, likely to bite), MEDIUM (missing test or maintainability concern), LOW (nit).

5. **Report.** For each finding, give the file, line number, what's wrong, and why it matters. Group by severity, most severe first. If nothing of note was found, say so plainly rather than inventing filler issues.

Do not modify any files, run fixes, or commit anything — this command only reports.
