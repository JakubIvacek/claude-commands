---
description: List available custom slash commands with a one-sentence summary of what each does
---

List the custom slash commands available globally. Follow these steps:

1. **Find the command files.** Check `~/.claude/commands/*.md`. Skip anything that isn't a `.md` file with a `description` frontmatter field. Don't look at any project-local `.claude/commands/` — this command only reports the global set.

2. **Read each file's frontmatter `description`.** That field is already a one-sentence summary written for this exact purpose — use it verbatim, don't rewrite or shorten it further. If a file has no `description` frontmatter, skip it rather than guessing at what it does.

3. **Print a clean list**, sorted alphabetically by command name, one line each:

   ```
   /commandname — description
   ```

4. If no command files are found, say so plainly instead of printing an empty list.

This command is read-only — it never edits, creates, or deletes files.
