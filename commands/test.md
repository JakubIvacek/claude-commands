---
description: "Inspect the project's testing setup, add or improve tests for the described functionality, run the suite, and report remaining coverage gaps."
argument-hint: "<functionality to test>"
---

Add or improve tests for: $ARGUMENTS

Follow these steps:

1. **Understand what needs covering.** Locate the code implementing the described functionality. If the description is vague, find the most relevant module/component by name or behavior before writing anything.

2. **Inspect the existing testing setup.** Identify the test framework and runner in use (check `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, etc.), the assertion/mocking style already used in nearby tests, and where tests live relative to source (colocated vs. a separate `tests/` tree). Match the project's existing conventions rather than introducing a new pattern.

3. **Identify gaps.** For the described functionality, check what's already tested and what's missing: happy path, error handling, edge cases (empty/null/boundary values), and branch coverage (each conditional path).

4. **Write tests to close the gaps.** Use descriptive test names that state the behavior under test. Keep each test independent — no shared mutable state. Mock external dependencies (network, filesystem, database) the way the existing suite already does.

5. **Run the relevant test suite** (not necessarily the whole repo if it's large/slow — scope to what's affected) and confirm the new tests pass and nothing else broke.

6. **Report.** Summarize what was added, confirm the suite is green, and call out any remaining coverage gaps you deliberately left (e.g. things that need a bigger fixture or fall outside this task's scope) rather than silently leaving them uncovered.

This command doesn't refactor implementation code to make it "more testable" beyond what's needed to write the test — that's a separate task if genuinely warranted.
