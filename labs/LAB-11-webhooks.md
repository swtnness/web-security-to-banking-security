# Lab 11 — Process synthetic payment events once

**Week:** 14. **Target:** offline toy, no payment provider. **Time:** two sessions.

This exercise begins **after an imagined verified event boundary**. It does not validate signatures, timestamps, origin, account environment or secrets. Never accept a caller-supplied “verified” flag in a real endpoint. Real integration must use the provider's verification procedure before business processing.

Save as `exercises/finance/events.py` and run `python events.py`:

~~~python
from copy import deepcopy

orders = {"O-1": {
    "payment": "P-1", "amount": 2500, "currency": "USD",
    "status": "pending", "fulfillments": 0,
}}
seen = {}

def process_synthetic(event):
    order = orders.get(event["order"])
    if order is None:
        raise ValueError("unknown order")
    if type(event["amount"]) is not int:
        raise ValueError("amount must be integer minor units")
    if (event["payment"], event["amount"], event["currency"]) != (
        order["payment"], order["amount"], order["currency"]
    ):
        raise ValueError("payment details mismatch")
    if event["type"] not in ("pending", "succeeded"):
        raise ValueError("unsupported event")
    fingerprint = tuple(event[field] for field in (
        "order", "payment", "amount", "currency", "type"
    ))
    if event["id"] in seen:
        if seen[event["id"]] != fingerprint:
            raise ValueError("event ID reused with different details")
        return "duplicate"
    if event["type"] == "succeeded" and order["status"] != "paid":
        order["status"] = "paid"
        order["fulfillments"] += 1
    # A late pending event cannot move a paid order backwards.
    seen[event["id"]] = fingerprint
    return order["status"]

base = {
    "id": "E-1", "order": "O-1", "payment": "P-1",
    "amount": 2500, "currency": "USD", "type": "succeeded",
}
assert process_synthetic(base) == "paid"
assert process_synthetic(base) == "duplicate"
assert process_synthetic(dict(base, id="E-2")) == "paid"
assert process_synthetic(dict(base, id="E-3", type="pending")) == "paid"

for altered in (
    dict(base, id="E-4", amount=1),
    dict(base, id="E-5", currency="EUR"),
    dict(base, id="E-6", order="O-2"),
    dict(base, id="E-7", payment="P-2"),
    dict(base, type="pending"),
):
    before = deepcopy((orders, seen))
    try:
        process_synthetic(altered)
    except ValueError:
        assert (orders, seen) == before
    else:
        raise AssertionError("expected rejection")

assert orders["O-1"]["fulfillments"] == 1
print("PASS: matching, duplicate events and late-event handling")
print(orders["O-1"])
~~~

Expected: one fulfillment and status paid. The example event schema is invented for this lesson; it is not a Stripe payload. Refunds, disputes and reversals need separately designed transitions and are outside this toy.

## Integration test plan

| Case | Required behavior | Evidence here |
|---|---|---|
| Invalid signature or wrong endpoint secret | Reject before business processing | Planned only |
| Timestamp outside accepted provider window | Apply provider replay policy | Planned only |
| Repeated valid event | No extra fulfillment | Executed by toy |
| New event ID for same completed payment | No extra fulfillment | Executed by toy |
| Wrong order/payment/amount/currency | No update | Executed by toy |
| Late pending after paid | No downgrade | Executed by toy |
| Concurrent workers or process restart | Durable deduplication and recoverable effects | Planned only |

In a real service, atomically record the event and transition; make fulfillment recoverable (for example, through a durable work queue/outbox and an idempotent worker). Reconcile with authoritative provider records. See [Stripe's webhook guide](https://docs.stripe.com/webhooks) for that provider's protocol.

**Save:** actual output and a diagram of the missing verification/durability boundary.

[Week 14](../curriculum/WEEK-14.md)

