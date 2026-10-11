# Week 13 — Transfer authorization, retries and concurrency

**Prerequisites:** Week 12 model and Python basics.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

A retry is not necessarily a new transfer. A valid authorization must apply to specific details. A concurrency safeguard must protect the balance decision and writes together; separate checks are not enough.

## Do these sessions in order

1. **Day 1.** Read [Module 2](../04-banking-security/02-money-movement.md). Define the allowed states and write five transfer invariants.

2. **Day 2.** Run [Lab 10](../labs/LAB-10-transfers.md)'s sequential transfer simulation. Predict the balances before reading the output.

3. **Day 3.** Test a same-key retry, a changed-payload reuse, wrong owner, zero/negative amount and insufficient balance. Confirm denial leaves the state unchanged.

4. **Day 4.** Complete the two-request interleaving exercise. Explain the overspend possible when two requests both see the same old balance.

5. **Day 5.** Write a database implementation plan: atomic ledger changes, a unique idempotency constraint, payload binding, serialization/locking and durable results. Identify what the toy code does not prove.

6. **Day 6.** Draw authorization expiry and detail changes as state transitions. Add one case that must require renewed approval and one canceled transaction case.

## Evidence

Save `progress/lab-10-report.md` with actual simulation output, the interleaving table and explicitly untested concurrency controls.

## Checkpoint

Can you explain why in-memory sequential deduplication is insufficient for concurrent or restarted servers?

Reading: [Stripe idempotent requests](https://docs.stripe.com/api/idempotent_requests) as a provider-specific reference.

[Previous](WEEK-12.md) · [Next](WEEK-14.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

