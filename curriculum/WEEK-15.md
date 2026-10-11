# Week 15 — Fraud signals, audit trails and incident response

**Prerequisites:** Weeks 12–14 threat and payment models.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

A fraud signal is evidence to investigate, not proof of wrongdoing. A response plan needs an owner, a trigger, a proportionate action and a recovery check. Logs should support an investigation without exposing unnecessary personal data.

## Do these sessions in order

1. **Day 1.** Read [Module 4](../04-banking-security/04-monitoring-and-response.md) and [Lab 12](../labs/LAB-12-incident.md). Identify the meaning of every synthetic event field.

2. **Day 2.** Build a timeline of the provided events. Distinguish authentication events, transfer decisions and reconciliation signals.

3. **Day 3.** Propose three detection rules and name at least one false positive for each. Specify the time window, grouping key and review action.

4. **Day 4.** Run the tabletop incident at each time step: triage, contain the affected account/session, preserve evidence and check for further exposure.

5. **Day 5.** Write recovery criteria: restore legitimate access, reconcile ledger/payment state and verify alerts. Do not erase audit records to clean up the incident.

6. **Day 6.** Write a short post-incident report with facts, hypotheses, unknowns, owners and a retest date. Redact identifiers as if this were a public portfolio.

## Evidence

Save `progress/lab-12-report.md` with a timeline, detection rules and a response playbook.

## Checkpoint

Can a second person follow the playbook without guessing who acts or how recovery is confirmed?

Reading: [OWASP logging guidance](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html).

[Previous](WEEK-14.md) · [Next](WEEK-16.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

