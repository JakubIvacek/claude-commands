# claude-commands

Personal [Claude Code](https://claude.com/claude-code) slash commands, shared in case they're useful to someone else.

## Commands

- **`/release`** — writes changes to project docs (TODO/backlog, spec files) where it makes sense, creating a minimal `CHANGELOG.md` as a fallback when the repo has no backlog or changelog file yet, bumps the app version (semver), verifies the build/tests pass, then commits and pushes. Works in any repo; it looks for the relevant files/scripts rather than assuming a fixed project layout.
- **`/implement`** — takes a feature/task description (`/implement <what to build>`), explores the project to understand conventions and where the work fits, breaks it down into a concrete plan, implements it in verified iterations (screenshots for UI, build/tests otherwise), then summarizes what was done and asks "did I forget anything?". It never writes docs or commits — that's `/release`'s job.
- **`/fix`** — takes a bug report or error (`/fix <description or error>`), reproduces it before touching code, traces it to the root cause (not just the symptom), applies the minimal fix, and checks for regressions. No refactoring or scope creep along the way. It never writes docs or commits either.
- **`/stale`** — audits whether `CLAUDE.md`/`README`/spec docs still match the actual code: checks each factual claim against the codebase and reports what's wrong or missing, grouped by file, and writes the findings to `.claude-stale-report.md`. Report-only — it never edits anything.
- **`/refresh`** — the fix-it counterpart to `/stale`: reads `.claude-stale-report.md` and edits the docs to match reality, matching the existing style, then deletes the report. Refuses to run (and asks you to run `/stale` first) if there's no report to work from.
- **`/uidesign`** — installs the taste, redesign, and ui-ux-pro-max design skills into this project's `.claude/skills/` (project scope, non-interactive).
- **`/list`** — lists the available custom slash commands with a one-sentence summary of each, pulled from their frontmatter `description`.
- **`/review`** — reviews the current branch or working-tree changes against a target branch for bugs, regressions, edge cases, missing tests, and maintainability issues. Report-only, like `/stale` — it never edits anything.
- **`/test`** — takes a description of functionality (`/test <what to cover>`), inspects the project's existing testing setup, adds or improves tests to match, runs the suite, and reports any remaining coverage gaps.
- **`/commit`** — inspects the current changes, splits unrelated work into separate logical commits when appropriate, and writes clear commit messages in the repo's existing style. Never pushes unless explicitly asked.
- **`/refactor`** — takes a description of what to refactor (`/refactor <what>`), identifies the existing invariants first, restructures the code incrementally without changing behavior, and verifies with tests at each step.
- **`/security`** — audits the described code or current changes (`/security [what]`) for auth gaps, input validation, secret exposure, dependency risk, and other OWASP-class vulnerabilities. Report-only by default; only fixes if explicitly asked.
- **`/prompt`** — takes a rough idea (`/prompt <idea>`, e.g. "redesign my landing page"), explores the project just enough to ground it in specifics, and outputs a single detailed, copy-pasteable prompt for another command like `/implement` or `/fix`. Never does the work itself.
- **`/todo`** — takes a rough idea (`/todo <idea>`), refines it into a concrete backlog entry grounded in the actual codebase, and adds it to the project's `TODO.md`/`BACKLOG.md` (matching its existing style), or creates a minimal `TODO.md` if none exists. Only touches that one file — no code, no other docs, no commits.

`CLAUDE.md` is the global instructions file this setup uses to point Claude Code at the available commands.

## Install

Copy the files into your global Claude Code config directory:

**Linux/macOS:**

```sh
cp commands/*.md ~/.claude/commands/
cp CLAUDE.md ~/.claude/CLAUDE.md   # or merge into your existing global CLAUDE.md
```

**Windows (PowerShell):**

```powershell
Copy-Item commands\*.md "$env:USERPROFILE\.claude\commands\"
Copy-Item CLAUDE.md "$env:USERPROFILE\.claude\CLAUDE.md"   # or merge into your existing global CLAUDE.md
```

Commands are then available as `/release`, `/implement`, `/fix`, `/stale`, `/refresh`, `/uidesign`, `/list`, `/review`, `/test`, `/commit`, `/refactor`, `/security`, `/prompt`, and `/todo` in any repo.
