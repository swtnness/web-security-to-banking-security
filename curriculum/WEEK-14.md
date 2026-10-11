# Week 14 — Payments, webhooks and data minimization

**Prerequisites:** Week 13 transfer invariants and retry semantics.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

Payment confirmation must come from trusted server-side evidence, not a browser success screen. Provider events may repeat or arrive out of order. Minimize sensitive data and decide exactly which system owns each payment state.

## Do these sessions in order

1. **Day 1.** Read [Module 3](../04-banking-security/03-payments-and-data.md). Draw browser → hosted checkout and provider → server event flow. Keep it fictional.

2. **Day 2.** List data your app needs: internal order ID, provider reference, expected amount, currency and status. Explain why raw card details are absent.

3. **Day 3.** Run [Lab 11](../labs/LAB-11-webhooks.md)'s event-processing simulation. It makes no provider connection and performs no payment.

4. **Day 4.** Complete signature, replay, duplicate, wrong-order, wrong-currency and amount-mismatch test plans. Mark cryptographic verification as planned, not implemented in the toy.

5. **Day 5.** Read the official PCI DSS overview. Write one paragraph on why architecture affects scope and why hosted checkout does not establish compliance by itself.

6. **Day 6.** Document reconciliation: what happens if the payment provider and internal order state disagree? Assign a human review owner and preserve both records.

## Evidence

Save `progress/lab-11-report.md` and a payment/data-flow design. No real card numbers or provider keys.

## Checkpoint

Can a changed browser total, repeated event or late pending event falsely mark an order paid in your model? Explain each guard.

Reading: [Stripe webhooks](https://docs.stripe.com/webhooks) and [PCI SSC overview](https://www.pcisecuritystandards.org/standards/pci-dss/).

[Previous](WEEK-13.md) · [Next](WEEK-15.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

