# Global instructions — UserName

Applies to every project on this machine (not just one specific repo). Specific recurring tasks (e.g. release) live as slash commands in `~/.claude/commands/` — this file is only for durable preferences/conventions that should always apply, not on-demand actions.

## Available global commands

- `/release` — write changes to docs, bump the app version, verify the build, commit + push. Works in any repo (`~/.claude/commands/release.md`).
- `/implement` — implement a feature/task from a description: explores the project, fleshes out the ask, implements it in iterations, and verifies the result. Works in any repo (`~/.claude/commands/implement.md`).
- `/fix` — fix a described bug: reproduce it, find the root cause, fix it minimally, verify no regressions. Works in any repo (`~/.claude/commands/fix.md`).
- `/stale` — audit whether CLAUDE.md/README/spec docs still match the actual code; reports drift, changes nothing. Works in any repo (`~/.claude/commands/stale.md`).
- `/refresh` — fixes the drift `/stale` found: edits the docs to match reality. Works in any repo (`~/.claude/commands/refresh.md`).
- `/todo` — refine a rough idea into a backlog entry and add it to the project's TODO/backlog file, creating one if none exists. Works in any repo (`~/.claude/commands/todo.md`).
