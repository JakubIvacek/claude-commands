---
description: "Refine a rough idea into a backlog entry and add it to the project's TODO/backlog file, creating one if none exists"
argument-hint: "<rough idea, e.g. \"add dark mode toggle\">"
---

Add this to the project's backlog: $ARGUMENTS

This command only writes to the project's backlog file. It never touches code, other documentation, or git — no commits, no pushes. Follow these steps:

1. **Find the project's existing backlog file, if any.** Check common names (`TODO.md`, `BACKLOG.md`, `TODOS.md`), and also check whether the project already keeps a "Backlog"/"TODO" section inside another doc (e.g. `README.md`). Don't assume a fixed name or location — look for what this specific project actually uses.

2. **Refine the rough idea into a concrete, actionable entry.** Skim the parts of the codebase the idea touches (grep for related files/components/functions) to ground it — note what already exists vs. what's actually missing, resolve any obvious ambiguity, and word the entry specifically enough that someone picking it up later (with no memory of this conversation) knows exactly what to build. Don't just restate the user's rough text verbatim.

3. **Check for an existing duplicate.** Before adding anything, check whether the backlog already has an entry describing the same thing. If so, update or merge into that existing line instead of adding a new one.

4. **If a backlog file exists:** append the refined entry matching its existing style exactly — same bullet format, same section/heading it belongs under, same tagging or priority conventions already in use. Don't invent new sections or formats the file doesn't already have.

5. **If no backlog file exists anywhere in the project:** create `TODO.md` at the repo root with a minimal structure — a single `## Backlog` heading and the refined entry as the first bullet. Don't add Done/In Progress/Priority sections or columns unless the idea itself implies that structure is needed.

6. **Report back.** State exactly what was added or changed and where (file path + section/line), so the user can review it before it's committed. Don't stage or commit the change — that's `/commit`'s or `/release`'s job.
