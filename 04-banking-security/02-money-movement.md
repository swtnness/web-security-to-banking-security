# Module 2 — Protect the intent and the ledger

**Week 13.** Work with fake USD minor units: 100 means USD 1.00 in this exercise. This convention is specific to the chosen currency; do not assume every currency has two decimal places.

## Transaction approval

For the fictional design, use:

~~~text
draft → pending approval → approved → executed
                    ↘ expired / canceled
~~~

Server policy determines allowed transitions. Bind approval to the authenticated actor, source, beneficiary, amount, currency, transaction identifier and relevant expiry. If significant details change, require a new approval. Check approval again at execution and consume it appropriately so replay cannot create another transfer.

Login and transaction approval have different purposes. The user should understand which action they are approving. This design follows the principles in [OWASP transaction authorization](https://cheatsheetseries.owasp.org/cheatsheets/Transaction_Authorization_Cheat_Sheet.html); the course does not implement a real approval channel.

## Exercise invariants

1. Only the authorized owner can debit the source account.
2. Amount is a positive integer in the selected currency's minor units.
3. A successful internal transfer reduces one balance and increases the other by the same amount.
4. No supported operation creates a negative balance in this no-overdraft model.
5. A denied operation leaves balances and entries unchanged.
6. A repeated intent with the same idempotency key has no additional effect.
7. Reusing a key with different details is rejected.
8. Each committed transfer has a traceable pair of entries.

These are requirements of this simplified model. Fees, FX, overdrafts, holds, reversals and external settlement require additional accounting rules.

## The concurrency problem

Balance is 100. Request X wants 80; request Y wants 80. If both read 100 before either writes, both can decide the transfer is affordable. That decision becomes unsafe when separated from the update.

A real implementation must choose appropriate database transactions and concurrency controls, such as row locks or serializable execution with retries. The balance decision, ledger entries and durable idempotency result need a coordinated atomic boundary. A unique key constraint must arbitrate competing requests.

## Retrying versus replay

Scope an idempotency key to the authenticated actor and operation. Bind it to the request's significant details and preserve a durable result for a documented retry period. A key is not an authenticator. Re-authenticate the requester before returning a stored result. Expired approval is a separate matter from safe transport retry.

[Stripe's idempotency documentation](https://docs.stripe.com/api/idempotent_requests) is a provider-specific example; its retention and error behavior should not be assumed universal.

## Do

Run [Lab 10](../labs/LAB-10-transfers.md). Then create a test plan for simultaneous requests, process crashes before/after commit and retries after restart. Mark those cases **not executed** in this in-memory exercise.

