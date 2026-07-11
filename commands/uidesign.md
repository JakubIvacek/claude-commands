---
description: Install the taste, redesign, and ui-ux-pro-max design skills into this project
---

Install these three design skills into this project's `.claude/skills/` (project scope, non-interactive), running each via Bash:

```
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend" -y
npx skills add https://github.com/Leonxlnx/taste-skill --skill "redesign-existing-projects" -y
npx skills add https://github.com/nextlevelbuilder/ui-ux-pro-max-skill -y
```

Run all three exactly as shown, in order. Do not substitute the `skillinstall` shell function — it isn't available to the Bash tool. If any command fails (e.g. `ui-ux-pro-max-skill` not found via `npx skills add` — it may only be installable as a plugin marketplace: `/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill`), report the failure and try that fallback rather than silently skipping it.

After all three finish, list what's now in `.claude/skills/` to confirm.