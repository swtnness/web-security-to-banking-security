# How to protect a website: controls and proof

Use after the foundation lessons. For each row record **tested / partial / planned / not applicable**, the evidence and remaining risk. A checked box without evidence is a reminder, not a security assessment.

| Area | Control | How to verify | Notes-app coverage |
|---|---|---|---|
| Authentication | Use framework password verification and sessions | Wrong password fails; correct one succeeds | Lab 08 |
| Account recovery | Expiring, single-use recovery with abuse controls | Expired/reused tokens fail | Design only |
| MFA and sensitive actions | Appropriate stronger verification | Step-up cannot be skipped or reused for changed details | Design only |
| Object access | Server checks actor, action and target | Bob cannot read/edit/delete Alice's note | Labs 07–08 |
| Ownership assignment | Set owner from verified actor | Client-supplied owner does not change ownership | Lab 08 |
| SQL | Parameterized queries / ORM without unsafe raw concatenation | SQL-looking value stays data | Lab 04; ORM in Lab 07 |
| Validation | Enforce length, type and business rules server-side | Empty/overlong body rejected | Lab 08 |
| Browser output | Escape text for its context | Markup appears literally | Labs 05, 08 |
| CSRF | Framework protection on state changes | Missing/invalid token rejected; valid token works | Lab 08 |
| Request methods | No destructive GET endpoints | GET delete leaves object intact | Lab 08 |
| Sessions | Rotate/revoke as appropriate; restrict cookie exposure | Logout denies access; inspect cookie attributes | Partial |
| Transport | Validated HTTPS and secure cookies | Review deployed TLS and response configuration | Planned |
| Browser headers | Appropriate framing, content-type and other policies | Inspect actual responses; test needed behavior | Lab 09, partial |
| Secrets | External secret storage; no public keys/tokens | Review diff and deployment configuration | Local review only |
| API | Object/function permission checks; limited fields | Guest/owner/non-owner matrix | Read-only endpoint tested |
| Rate limiting | Bound expensive or sensitive operations | Controlled abuse tests and recovery path | Planned |
| Dependencies | Record versions, patch and rerun tests | Reviewed update with passing regression suite | Maintenance exercise |
| Files and outbound requests | Constrain uploads, paths and server fetches | Reject unsafe types/paths/destinations | Not implemented |
| Logging | Useful events with limited sensitive data | Verify allowed/denied events; inspect fields | Lab 09, partial |
| Backups and resilience | Protected copies and tested restore | Restore drill and reconciliation | Planned |
| Incident response | Named roles, triggers and recovery criteria | Tabletop with recorded decisions | Lab 12 |

## Reviewing code

Trace a single request from route to authentication, validation, authorization, database operation, response and log. Check all alternative routes to the same object. Read tests that verify the rejected operation did not change state.

Do not assume a framework, WAF, scanner or HTTPS makes every operation safe. Match each identified threat to a specific enforced control.

## Before public deployment

The course app is local. A public service needs a stable external secret, DEBUG=False, appropriate hosts, HTTPS, suitable hosting, abuse controls, recovery design, monitoring, backup testing and independent review. Do not publish the course server as-is.

Use [Django's deployment checklist](https://docs.djangoproject.com/en/5.2/howto/deployment/checklist/) for that framework. Use [OWASP ASVS](https://owasp.org/projects/asvs) to select broader requirements, recording the version and exact IDs you consulted.

[Curriculum](../curriculum/ROADMAP.md)

