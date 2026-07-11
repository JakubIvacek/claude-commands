---
description: "Audit the described code or current changes for auth, input validation, secret exposure, dependency risk, and common vulnerabilities. Reports findings only unless asked to fix."
argument-hint: "[what to audit, default: current changes]"
---

Security audit: $ARGUMENTS

This is a report-only audit by default — only fix issues if explicitly asked to. Follow these steps:

1. **Scope the review.** If `$ARGUMENTS` names specific code, review that. Otherwise default to `git diff` against the current changes (staged + unstaged); if there are none, ask what to audit.

2. **Read the relevant files in full**, not just diff hunks — auth and validation bugs are often visible only with surrounding context (e.g. a check that exists elsewhere in the file but isn't applied here).

3. **Check for:**
   - **Authentication / authorization** — missing checks, privilege escalation paths, broken access control, tokens/sessions handled insecurely
   - **Input validation** — unvalidated user input reaching a query, shell command, file path, or template; SQL/command/path injection; XSS
   - **Secret exposure** — hardcoded API keys, tokens, passwords, credentials committed to source or logs
   - **Dependency risk** — newly added or updated dependencies with known CVEs, or packages pulled from untrusted sources
   - **Other OWASP-class issues** — SSRF, insecure deserialization, weak/misused cryptography, CSRF gaps, verbose error messages leaking internals

4. **Assign severity**: CRITICAL (exploitable now, must fix before merge), HIGH (real risk, should fix), MEDIUM (defense-in-depth gap), LOW (hardening suggestion).

5. **Report.** For each finding: file, line, what's wrong, how it could be exploited, and the fix. Group by severity, most severe first. If genuinely nothing is found, say so rather than manufacturing low-value nits.

6. **Only fix if explicitly asked.** If asked to fix, apply the minimal change that closes the vulnerability — no unrelated refactoring — and re-state which findings were fixed vs. left for the user to address (e.g. things requiring a design decision, like key rotation).
