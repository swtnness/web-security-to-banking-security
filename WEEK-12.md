# Week 12 — Model a fictional bank and its assets

**Prerequisites:** Weeks 1–11: authorization, data access, tests and limitations.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

Money movement adds integrity and accountability requirements. The client displays data; authoritative balances and ownership decisions belong on the server. A ledger, an audit trail and a fraud signal serve different purposes.

## Do these sessions in order

1. **Day 1.** Read [the financial roadmap](../04-banking-security/BANKING-ROADMAP.md) and [Module 1](../04-banking-security/01-threat-model.md). Define the fictional system's scope.

2. **Day 2.** Draw the browser, identity service, API, ledger, notification service and mocked payment provider. Label trust boundaries and authoritative records.

3. **Day 3.** List fake customers, accounts, transactions and roles. Separate support access from transfer permission and reconciliation duties.

4. **Day 4.** Write six abuse cases: account takeover, object authorization failure, amount change, duplicate delivery, concurrent spending and leaked logs.

5. **Day 5.** For each abuse case, add a prevention, a detection and a negative test. Reuse the threat-model template but replace the web-notes assumptions.

6. **Day 6.** Review Module 2's transaction lifecycle. Explain the difference between logging in, being allowed to debit an account and approving specific transfer details.

## Evidence

Save `progress/week-12.md` with a labeled diagram, asset inventory and at least six threat rows.

## Checkpoint

Can you name the authoritative record for balances and show why a browser-submitted balance is ignored?

Reading: [OWASP transaction authorization](https://cheatsheetseries.owasp.org/cheatsheets/Transaction_Authorization_Cheat_Sheet.html).

[Previous](WEEK-11.md) · [Next](WEEK-13.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

