# Module 4 — Detect, investigate and recover

**Week 15.** Separate prevention, detection and response. A blocked transfer and a completed transfer should not trigger the same financial recovery action.

## Useful events

Record event time, a stable event ID, synthetic actor/account reference, action, decision, reason code and a correlation identifier. Distinguish when an event happened from when it was received. Avoid credentials, raw session IDs, complete payment data and unnecessary user input.

Restrict log access, protect integrity, monitor collection failures and define retention by purpose and applicable obligations. A console printout alone is not an audit system. See [OWASP logging guidance](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html).

## Three example hypotheses

| Signal | Why investigate | Possible benign explanation |
|---|---|---|
| Several login failures followed by success | Password guessing or account takeover | A user forgot a password |
| Recovery-factor change followed by a new beneficiary | Control of both account and money destination may have changed | A legitimate phone replacement |
| Many small transfers close together | Abuse, automation or a broken integration | Normal scheduled activity |

Choose thresholds for the fictional dataset and label them educational assumptions. Risk scoring must be tested for false positives and customer harm; “unusual” does not mean “fraudulent.”

## Response structure

- **Triage owner:** verify whether events belong to the same actor and session, and distinguish facts from hypotheses.
- **Containment owner:** restrict the affected session or transaction capability according to policy; preserve legitimate access where possible.
- **Evidence owner:** preserve records and record decisions without modifying the ledger to hide activity.
- **Finance/reconciliation owner:** compare expected entries and provider records before deciding whether a correction is needed.
- **Recovery owner:** restore access through a verified process, check invariants and monitor recurrence.
- **Review owner:** identify root cause, assign fixes and define retests.

Practice these roles yourself in the tabletop; they are fictional roles, not actual people to contact.

## Do

Use [Lab 12](../labs/LAB-12-incident.md) to build a timeline and a response playbook. Write what you would do if a suspicion is disproved. Record gaps such as missing session correlation instead of filling them with guesses.

