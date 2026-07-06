---
description: Audit whether CLAUDE.md/README/spec docs still match the actual code — reports drift, changes nothing
---

Audit whether this repo's documentation still matches reality. This is a **report-only** command — do not edit any files.

1. **Find the docs that make factual claims about the code.** Typically `CLAUDE.md`, `README.md`, `ARCHITECTURE.md`, or similar spec/convention files — anything that describes behavior, data model, architecture, setup steps, or conventions (not changelogs or backlogs, those are expected to be historical).

2. **Check each factual claim against the actual code.** For each concrete, checkable statement (a file path, a function/component name, a data model field, a build command, a described behavior, a listed convention), verify it against the current codebase — read the relevant file, grep for the symbol, run the command if it's cheap and safe (e.g. `--help`, not something destructive). Don't just skim; a claim that "sounds plausible" is not the same as one you verified.

3. **Classify what you find** into:
   - **Wrong** — the doc states something that is no longer true (renamed/removed file, changed behavior, stale command).
   - **Missing** — the code has grown a feature/convention/module that no relevant doc mentions at all.
   - **Vague/unverifiable** — claims too generic to check either way (skip these, don't pad the report).

4. **Report back, don't fix.** For each "wrong" or "missing" item: cite the doc file + line, cite the code evidence that contradicts or is missing from it, and give a one-line suggested correction. Group by file. If everything checks out, say so plainly — don't invent nitpicks to justify the audit.

5. **Write the findings to `.claude-stale-report.md` in the repo root**, grouped by doc file, same content as the chat report (skip this file entirely if there were zero findings). If the repo has a `.gitignore` and doesn't already ignore this filename, add a line for it — this file is a working artifact, not something to commit.

If the user wants the drift actually fixed, run `/refresh` — it consumes this report so the fix pass doesn't need to redo the audit.