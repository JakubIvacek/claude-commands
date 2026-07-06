---
description: Implement a feature/task from a description — explores the project, fleshes out the ask, implements it in iterations, and verifies the result
---

Implement this: $ARGUMENTS

Follow these steps:

1. **Understand the ask.** Read CLAUDE.md/README/TODO and explore the relevant code (use an Explore agent if you're not sure where something lives) to figure out exactly what's meant — conventions, existing patterns, where this fits into the architecture, whether something similar already exists. If, after exploring, the ask is still ambiguous in a way that meaningfully changes the outcome (not cosmetic), ask before writing any code — don't guess.

2. **Flesh the ask out into a concrete plan.** Work out exactly what needs to happen — which files, what behavior changes, edge cases, what touches UI/store/DB, what needs to be added to i18n, etc. (whatever's relevant for this project). Prepare a TODO list (TodoWrite) with the steps. For anything non-trivial, consider Plan mode and get the plan approved before touching code.

3. **Implement incrementally, in iterations.** Don't do it all in one shot — break it into logical steps (2-3 iterations as a baseline, more if the task is bigger), and after each iteration verify that what you built actually works:
   - For anything visual/UI, run the app and check it for real — screenshot / walk the flow in a browser (the `run` skill).
   - If a typecheck/build/test is enough, verify with that (find the actual commands from `package.json`/a Makefile etc., don't assume blindly).
   - If something doesn't work or doesn't match the ask, fix it in the next iteration before moving on.

4. **At the end, summarize what you did and self-check.** Go back over the original ask and check whether you missed any part, edge case, or common related concern (i18n strings, dark mode, responsive layout, empty/error states, etc. — whatever's relevant for the project). In the summary, state:
   - what's done,
   - what you knowingly left out/deferred and why,
   - and explicitly ask: "Did I forget anything?" — call out specific things you're unsure whether the user wanted included.

This command doesn't write to documentation or bump the version/commit/push — that's what `/release` is for; run it separately once the implementation is verified and you want to ship it.
