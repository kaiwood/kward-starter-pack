---
name: security-privacy
description: Use when changing auth, permissions, secrets, API endpoints, user input, uploads, cookies, redirects, logging, analytics, or personal data handling. Applies security and privacy guardrails without broad audits.
---

# Security Privacy

## Goal

Avoid introducing security or privacy regressions while keeping the review proportional to the change.

This is a guardrail, not a full security audit.

## Use This Skill When

- Changing login, logout, sessions, auth, OAuth, or API keys.
- Changing roles, permissions, ownership checks, or access control.
- Changing API endpoints, server actions, webhooks, or database queries.
- Handling user input, forms, search, uploads, files, URLs, or redirects.
- Touching cookies, CORS, CSRF, CSP, headers, or browser storage.
- Logging, analytics, error reporting, monitoring, or telemetry changes.
- Handling personal, sensitive, financial, health, location, or account data.
- Adding third-party scripts, SDKs, integrations, or dependencies.

## Usually Skip For

- Pure styling/layout changes.
- Copy-only changes.
- Local-only test helpers with no sensitive fixtures.
- Internal refactors that do not touch data, auth, network, or persistence boundaries.

## Core Rules

- Do not expose secrets, tokens, credentials, or private keys.
- Do not trust client-side checks for authorization.
- Validate and authorize on the server or trusted boundary.
- Prefer least privilege and fail-closed behavior.
- Do not log sensitive data.
- Keep personal data collection, retention, and sharing minimal.
- Avoid broad security abstractions unless they reduce real risk.
- Preserve existing security behavior unless the change explicitly requires otherwise.
- If unsure whether a change weakens security, stop and ask.

## Security Checklist

For relevant changes, check:

- **Auth:** Is identity established by a trusted mechanism?
- **Authorization:** Is access checked server-side for the specific resource/action?
- **Ownership:** Can one user access another user's data by changing an ID?
- **Input:** Are untrusted inputs validated, parsed, bounded, and encoded appropriately?
- **Output:** Is user-controlled content escaped or sanitized for the target context?
- **Secrets:** Are secrets kept out of source, logs, client bundles, and error messages?
- **Sessions/Cookies:** Are cookie/session settings appropriate for the app?
- **CSRF/CORS:** Are cross-origin and state-changing requests protected?
- **Redirects/URLs:** Are redirects and callback URLs constrained to trusted destinations?
- **Uploads/Files:** Are file type, size, path, and content handling constrained?
- **Database:** Are queries parameterized, scoped, and permission-filtered?
- **Dependencies:** Is a new dependency necessary and reasonably trusted?

## Privacy Checklist

For personal or sensitive data:

- Collect only what is needed.
- Store only what is needed.
- Retain only as long as needed.
- Avoid sending sensitive data to third-party services unless required.
- Avoid exposing personal data in logs, analytics, URLs, screenshots, or errors.
- Prefer anonymized, aggregated, or redacted data where practical.
- Keep test fixtures free of real personal data.

## Tests / Verification

When practical, add or update tests for:

- unauthorized access denial
- ownership/resource scoping
- invalid or malicious input
- redirect allowlists
- sensitive data redaction
- server-side enforcement, not only client UI hiding

Run focused verification first. Do not weaken security tests to pass.

## Common Red Flags

- Authorization only in the frontend.
- Returning data before checking permissions.
- Trusting request body user IDs, roles, prices, or ownership fields.
- Logging full request bodies, tokens, emails, addresses, or payment details.
- Putting secrets in env files committed to source control.
- Using `dangerouslySetInnerHTML`, raw SQL, shell commands, or dynamic eval with user input.
- Open redirects through `next`, `returnTo`, `callbackUrl`, or similar params.
- Overly broad CORS, cookie, or token scopes.
- Test fixtures copied from real user data.

## Final Report

For relevant work, briefly summarize:

```text
Security/privacy notes:
- Authorization remains server-side and resource-scoped.
- No secrets or personal data added to logs.
- Added regression test for unauthorized access.
```

If not relevant:

```text
Security/privacy: not relevant; change does not touch auth, data, network, persistence, or sensitive logging.
```
