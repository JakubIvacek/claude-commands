# claude-commands

Personal [Claude Code](https://claude.com/claude-code) slash commands, shared in case they're useful to someone else.

## Commands

- **`/release`** — writes changes to project docs (TODO/backlog, spec files) where it makes sense, bumps the app version (semver), verifies the build/tests pass, then commits and pushes. Works in any repo; it looks for the relevant files/scripts rather than assuming a fixed project layout.
- **`/implementation`** — takes a feature/task description (`/implementation <what to build>`), explores the project to understand conventions and where the work fits, breaks it down into a concrete plan, implements it in verified iterations (screenshots for UI, build/tests otherwise), then summarizes what was done and asks "did I forget anything?". It never writes docs or commits — that's `/release`'s job.

`CLAUDE.md` is the global instructions file this setup uses to point Claude Code at the available commands.

## Install

Copy the files into your global Claude Code config directory:

```sh
cp commands/*.md ~/.claude/commands/
cp CLAUDE.md ~/.claude/CLAUDE.md   # or merge into your existing global CLAUDE.md
```

Commands are then available as `/release` and `/implementation` in any repo.
