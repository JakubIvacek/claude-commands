---
description: "Inspect current changes, split unrelated work into logical commits when appropriate, and write clear commit messages. Never pushes unless explicitly requested."
argument-hint: "[optional notes on scope/intent]"
---

Commit the current changes. $ARGUMENTS

Follow these steps:

1. **Survey the changes.** Run `git status` and `git diff` (both staged and unstaged) to see everything that's changed, including untracked files.

2. **Group by logical unit.** If the changes clearly represent more than one unrelated piece of work (e.g. an unrelated bug fix mixed in with a feature, or a formatting pass mixed with logic changes), split them into separate commits by staging only the relevant files/hunks for each. If the changes are all one cohesive piece of work, make a single commit — don't split for the sake of splitting.

3. **Check for anything that shouldn't be committed.** Skip build artifacts, editor files, and anything that looks like a secret or credential (`.env`, keys, tokens) — warn the user if such a file appears staged or requested, rather than committing it silently.

4. **Stage deliberately.** Add specific files/paths by name; don't reach for blanket `git add -A`/`git add .` if the working tree has unrelated untracked content.

5. **Write each commit message** following this repo's existing convention (check `git log` for the prevailing style — conventional-commit prefixes like `feat:`/`fix:`/`refactor:` if that's what's used). Focus the message on *why*, not a restatement of the diff.

6. **Verify.** Run `git status` after committing to confirm the working tree is in the expected state and nothing was left uncommitted that should've been included (or vice versa).

7. **Do not push** unless the user explicitly asked for it in `$ARGUMENTS` or this message — commit only.
