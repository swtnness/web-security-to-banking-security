# Module 1 — Assets, identity and trust boundaries

**Week 12.** MiniBank lets fake customers view fake balances and propose internal transfers. Support can review limited account metadata; a separate finance role reviews reconciliation exceptions.

## Draw this architecture

~~~text
Untrusted browser
     | HTTPS / session / user input
     v
Application API ---- Identity/session service
     |
     +---- Account permissions
     |
     +---- Transfer service ---- Authoritative ledger/database
     |
     +---- Payment adapter ---- Mock external provider
     |
     +---- Limited audit events ---- Monitoring/review
~~~

Mark boundaries at browser→API, API→data store and provider→adapter. An internal network location is not proof of identity or permission.

## Define the assets

| Asset | Requirement | Example failure |
|---|---|---|
| Session and recovery channel | Only the right actor uses it | Account takeover through recovery |
| Account ownership | Verified for each action | Alice debits Bob's account |
| Transfer intent | Recipient, currency and amount remain bound to approval | Amount changes after approval |
| Ledger entries | Balanced, consistent and durable | Debit succeeds but credit is missing |
| Payment reference | Bound to the correct order and environment | A different order's success is reused |
| Audit evidence | Access-controlled and tamper-resistant | Harmful action is hidden or logs expose private data |

The browser may submit a requested amount, but cannot declare the true balance, account owner, approval status or settlement result.

## Identity is more than login

Distinguish identity proofing, authentication, account authorization and transaction approval. A recovery channel can become the weakest path; changing a phone, email or authenticator needs careful verification and notification. Do not collect real identity documents for this course.

## Assignment

Create six threat rows using [the template](../templates/THREAT-MODEL.md). For each: actor, precondition, asset, abuse action, effect, control, test, owner and residual risk.

Example: a compromised customer session initiates a transfer to a new beneficiary. A transaction confirmation bound to significant details and a proportionate risk review can reduce harm; neither proves the user's device is uncompromised.

**Done:** your diagram shows where balances originate, where ownership is checked, and where external events are authenticated.

Reading: [OWASP authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html).

