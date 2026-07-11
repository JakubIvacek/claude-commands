# claude-commands

Personal [Claude Code](https://claude.com/claude-code) slash commands, shared in case they're useful to someone else.

## Commands

- **`/release`** — writes changes to project docs (TODO/backlog, spec files) where it makes sense, bumps the app version (semver), verifies the build/tests pass, then commits and pushes. Works in any repo; it looks for the relevant files/scripts rather than assuming a fixed project layout.
- **`/implementation`** — takes a feature/task description (`/implementation <what to build>`), explores the project to understand conventions and where the work fits, breaks it down into a concrete plan, implements it in verified iterations (screenshots for UI, build/tests otherwise), then summarizes what was done and asks "did I forget anything?". It never writes docs or commits — that's `/release`'s job.
- **`/fix`** — takes a bug report or error (`/fix <description or error>`), reproduces it before touching code, traces it to the root cause (not just the symptom), applies the minimal fix, and checks for regressions. No refactoring or scope creep along the way. It never writes docs or commits either.
- **`/stale`** — audits whether `CLAUDE.md`/`README`/spec docs still match the actual code: checks each factual claim against the codebase and reports what's wrong or missing, grouped by file, and writes the findings to `.claude-stale-report.md`. Report-only — it never edits anything.
- **`/refresh`** — the fix-it counterpart to `/stale`: reads `.claude-stale-report.md` and edits the docs to match reality, matching the existing style, then deletes the report. Refuses to run (and asks you to run `/stale` first) if there's no report to work from.
- **`/uidesign`** — installs the taste, redesign, and ui-ux-pro-max design skills into this project's `.claude/skills/` (project scope, non-interactive).

`CLAUDE.md` is the global instructions file this setup uses to point Claude Code at the available commands.

## Install

Copy the files into your global Claude Code config directory:

```sh
cp commands/*.md ~/.claude/commands/
cp CLAUDE.md ~/.claude/CLAUDE.md   # or merge into your existing global CLAUDE.md
```

Commands are then available as `/release`, `/implementation`, `/fix`, `/stale`, `/refresh`, and `/uidesign` in any repo.
