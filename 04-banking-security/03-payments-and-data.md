# Module 3 — Payment confirmation and sensitive data

**Week 14.** Design a fictional checkout. No provider account, real card data or live charge is required.

## Draw two separate flows

1. The server creates an order using authoritative product prices and currency. The browser visits a provider-hosted checkout.
2. The provider sends an event to the application's backend. The backend verifies it, checks the expected order details, updates the order and later reconciles records.

A browser redirect saying “success” cannot authorize fulfillment. Amount, currency, internal order and provider payment reference must match the server's expected records.

## Webhook handling

Use the provider's official SDK and documented signature procedure on the raw request body, with the correct endpoint secret and environment. Apply the provider's timestamp/replay rules. Handle duplicate events and avoid assuming delivery order. Acknowledge delivery according to provider guidance after safely recording or processing it.

For Stripe specifically, consult [the webhook guide](https://docs.stripe.com/webhooks); other providers have different signing and retry protocols. The course's synthetic event processor deliberately starts **after** this verification boundary.

Separate duplicate delivery from duplicate business effect: two different event IDs can describe the same payment. Your order transition must not fulfill twice. Do not downgrade a paid order because a late pending event arrives.

## Keep less data

| Keep for the fictional order | Exclude from this repository |
|---|---|
| Synthetic order ID and provider reference | Real card numbers and security codes |
| Expected amount, currency and status | Provider secret keys |
| Limited timestamps and outcome codes | Session tokens and raw signed request captures |
| Reconciliation status | Real customer identity documents |

Tokenization replaces sensitive data with a controlled reference. Tokens may still be sensitive and require access control. Encryption needs key management, restricted access, rotation and recovery planning; do not invent payment cryptography.

## PCI DSS awareness

[PCI SSC](https://www.pcisecuritystandards.org/standards/pci-dss/) describes the standard for protecting payment account data. Applicability and validation depend on the entity and payment architecture. A hosted checkout may reduce exposure, but choosing one does not establish compliance. This course performs no compliance assessment and prescribes no jurisdiction-specific banking rules.

## Do

Complete [Lab 11](../labs/LAB-11-webhooks.md). Write a one-page flow showing verification, matching, deduplication, state transition and reconciliation. Add the signature verification and crash/retry cases as planned tests.

