---
description: Fix doc/code drift found by /stale — actually edits CLAUDE.md/README/spec docs to match reality
---

Refresh the documentation so it matches the actual code. Scope: $ARGUMENTS (if empty, the whole repo's docs).

This is the fix-it counterpart to `/stale`. Where `/stale` only reports, this command edits. The code is always the source of truth — you're correcting the docs to match the code, never the other way around.

1. **Get the drift list.** Check for `.claude-stale-report.md` in the repo root. If it doesn't exist, stop and ask the user to run `/stale` first — don't redo the audit yourself, that's `/stale`'s job and duplicating it here would drift the two commands apart over time.

2. **For each confirmed drift item, fix the doc, not the code.** If a doc names a file/function/field that was renamed or removed, update the name. If a doc describes behavior that changed, rewrite that description to match what the code actually does now. If the code has grown something a doc should mention but doesn't, add it — in the existing structure/section, not a new one.

3. **Match the existing style exactly.** Same tone, same level of detail, same formatting conventions as the surrounding doc. Don't restructure sections, invent new headings, or expand scope beyond correcting the drift — this is a correction pass, not a rewrite.

4. **Skip anything genuinely ambiguous.** If you can't tell what the doc *should* say (the intended behavior isn't obvious from the code alone), don't guess — flag it in your summary instead of writing something possibly wrong.

5. **Clean up.** Once every item in the report is addressed (or explicitly skipped), delete `.claude-stale-report.md` — a leftover report describing already-fixed drift is itself stale.

6. **Summarize what you changed, file by file** — old claim → corrected claim, one line each. Note anything you deliberately skipped and why.

This command doesn't bump the version, commit, or push — that's `/release`'s job, run it separately once you're happy with the doc changes.
