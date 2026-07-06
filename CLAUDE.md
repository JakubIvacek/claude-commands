# Global instructions — UserName

Applies to every project on this machine (not just one specific repo). Specific recurring tasks (e.g. release) live as slash commands in `~/.claude/commands/` — this file is only for durable preferences/conventions that should always apply, not on-demand actions.

## Available global commands

- `/release` — write changes to docs, bump the app version, verify the build, commit + push. Works in any repo (`~/.claude/commands/release.md`).
- `/implementation` — implement a feature/task from a description: explores the project, fleshes out the ask, implements it in iterations, and verifies the result. Works in any repo (`~/.claude/commands/implementation.md`).
- `/fix` — fix a described bug: reproduce it, find the root cause, fix it minimally, verify no regressions. Works in any repo (`~/.claude/commands/fix.md`).
