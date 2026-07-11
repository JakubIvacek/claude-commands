---
description: "Turn a rough idea into a detailed, project-grounded prompt you can copy into /implementation, /fix, or any other command. Does not do the task itself."
argument-hint: "<rough idea, e.g. \"redesign my landing page\">"
---

Turn this rough idea into a detailed prompt: $ARGUMENTS

This command never implements anything — it only researches enough to write a sharp, specific prompt, then hands it back for you to paste elsewhere (e.g. `/implementation <prompt>`, `/fix <prompt>`, or run as-is). Follow these steps:

1. **Parse the intent.** Figure out what kind of task this is (new feature, redesign, bug fix, refactor, etc.) — that shapes which command the output prompt is meant for, and what detail matters.

2. **Explore the project just enough to ground the prompt.** Don't do the work — look for the specifics that turn a vague ask into a concrete one:
   - Relevant files/components/pages already touching this area (e.g. for "redesign my landing page," find the actual landing page file(s), current layout, styling approach/framework)
   - Existing conventions to preserve (design system, component patterns, naming, tech stack)
   - Anything that constrains the request (existing tests to keep green, related open TODOs, adjacent code that will be affected)

3. **Ask yourself what's ambiguous.** If the rough idea leaves a real fork in approach (e.g. "redesign" could mean visual polish only vs. restructuring content/IA), don't silently guess — note the ambiguity directly in the generated prompt as an open question, or pick the most likely reading and say so explicitly, so the user can correct it before running the real command.

4. **Write the detailed prompt.** It should read as a self-contained instruction someone (or another Claude session) could execute without needing this conversation's context. Include:
   - A clear one-line statement of the goal
   - The specific files/areas in scope (with paths)
   - Concrete requirements pulled from the project's actual conventions (not generic advice)
   - Explicit constraints (what must not change/break)
   - Anything flagged as ambiguous in step 3

5. **Output only the prompt**, in a copy-pasteable block, prefixed with a one-line note on which command it's meant for (e.g. "Paste into `/implementation`:"). Don't pad it with your own commentary about the project outside of what belongs in the prompt itself.
