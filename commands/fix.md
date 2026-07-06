---
description: Fix a described bug — reproduce it, find the root cause, fix it minimally, verify no regressions
---

Fix this bug: $ARGUMENTS

This is different from `/implementation`: you are not building something new, you are removing a defect with the smallest change that actually fixes it. Follow these steps:

1. **Understand the report.** If given an error message/stack trace, locate exactly where it fires in the code and read the surrounding logic. If given a description ("X does Y when it should do Z"), find the code path responsible. Don't start editing yet.

2. **Reproduce it before touching any code.** Run the app, write a quick script, or run/write a failing test — whatever proves the bug is real and you're looking at the right thing. If you can't reproduce it from what you were given, say so and ask for more detail (exact steps, environment, input) instead of guessing at a fix blind.

3. **Find the root cause, not the first symptom.** Trace back from where the error/wrong behavior surfaces to why it actually happens. If the first plausible explanation doesn't fully account for the reproduced behavior, keep digging — a fix built on the wrong cause will look right and still be wrong.

4. **Fix it minimally.** Change only what's needed to address the root cause. No refactoring, no renaming, no "while I'm here" improvements, no touching unrelated code — even if you notice something else that looks off (mention it in your summary instead, don't fix it here).

5. **Verify the fix addresses the cause, not just the symptom.** Re-run the same repro/test from step 2 and confirm it now passes. If the project has a test suite, add a regression test for this specific case unless that's clearly overkill for the codebase's conventions.

6. **Check for regressions.** Run the existing build/test suite. Sanity-check other code paths that touch the same function/state/component — a fix that passes its own repro but breaks a sibling case isn't done.

7. **Summarize.** State what the actual root cause was (not just the visible symptom), what you changed, and how you verified it. If you spotted other issues along the way that you deliberately left alone, list them instead of fixing them.

This command doesn't write to documentation, bump the version, commit, or push — that's what `/release` is for.
