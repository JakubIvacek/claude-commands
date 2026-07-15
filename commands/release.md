---
description: Write changes to docs, bump app version, commit and push
---

Release the current changes in this repo. Follow these steps exactly:

1. **Find out what changed.** `git status` + `git diff` (+ `git log -1` for commit-style context). Summarize what actually changed — feature, fix, refactor, docs, i18n...

2. **Write the changes into documentation, but only where it makes sense:**
   - If the repo has a backlog/todo file (e.g. `TODO.md`, `BACKLOG.md`), move the completed item into the "done" section in the same style as existing entries, or add a new line.
   - If the repo has a bug tracker file (e.g. `BUGS.md`, `ISSUES.md`) and the change fixes a bug from there, remove/move that line.
   - If the repo has a spec/convention file (e.g. `CLAUDE.md`, `ARCHITECTURE.md`, `README.md`), update it **only** if the behavior/architecture/data model/setup it describes actually changed — not for a routine UI fix.
   - Don't invent new changelog sections or formats that weren't there before — stick to the file's existing style.
   - Before adding a new line, check whether this change is already mentioned in the file (e.g. an existing TODO line that describes the exact same thing) — if so, edit/move that existing line instead of adding a duplicate.
   - If no backlog/todo file and no changelog file exists anywhere in the repo, create a minimal `CHANGELOG.md` at the repo root (Keep a Changelog style: an `## Unreleased` heading with a bullet for this change) and add the entry there — running `/release` is itself the request to document the change, so this is the one doc file this step is allowed to create from scratch. Don't create or touch `TODO.md`, `BACKLOG.md`, `BUGS.md`, `ISSUES.md`, `CLAUDE.md`, `README.md`, or `ARCHITECTURE.md` as part of this fallback — those are only touched if they already exist (per the bullets above), and a missing `TODO.md`/`BACKLOG.md` is `/todo`'s job, not this one's.

3. **Bump the app version, if the repo has a version that's displayed or published somewhere** (typically `package.json` → `"version"`, possibly a hardcoded constant in the UI like `APP_VERSION`, or a `Cargo.toml`/`pyproject.toml` version, etc.). Find every place the version is duplicated and bump them all to the same number.
   - Semver: **patch** for a fix/small tweak, **minor** for a new feature, **major** only if explicitly requested.
   - If the project doesn't display/publish a version anywhere, skip this step.

4. **Verify the build/tests pass** (find the build/test command from `package.json` scripts, a Makefile, or similar — don't blindly assume `npm run build`, confirm such a script exists).

5. **Commit + push.**
   - One commit, a message in the style of the repo's existing commits (`git log --oneline` for inspiration) — factual, no fluff.
   - Include only files related to the change (no blind `git add -A`/`git add .`).
   - Push to the branch tracking the remote (typically `main`), unless told otherwise.

If you're unsure about something (patch vs. minor, whether something belongs in a spec file, what the build command is), ask before pushing — don't guess.