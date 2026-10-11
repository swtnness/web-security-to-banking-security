# Lab 10 — Transfer invariants and duplicate requests

**Week:** 13. **Target:** offline Python with fake USD minor units. **Time:** two sessions plus the tabletop. **Prerequisite:** Module 2.

This toy implements sequential ownership, validation, balanced entries and in-memory deduplication. It has no authentication channel, approval protocol, network, database, persistence or concurrency protection. The actor argument represents an already verified actor for the exercise.

Save as `exercises/finance/transfers.py` and run `python transfers.py`:

~~~python
from copy import deepcopy

owners = {"A": "alice", "B": "bob"}
balances = {"A": 10000, "B": 2000}
entries = []
receipts = {}

def transfer(actor, source, target, amount, key, currency="USD"):
    if source not in owners or target not in owners or source == target:
        raise ValueError("invalid accounts")
    if owners[source] != actor:
        raise PermissionError("source not owned")
    if type(amount) is not int or amount <= 0 or currency != "USD":
        raise ValueError("invalid money")
    if not isinstance(key, str) or not key or len(key) > 100:
        raise ValueError("invalid retry key")
    scope = (actor, key)
    intent = (source, target, amount, currency)
    if scope in receipts:
        previous_intent, result = receipts[scope]
        if intent != previous_intent:
            raise ValueError("key reused for different intent")
        return result
    if balances[source] < amount:
        raise ValueError("insufficient funds")
    # Sequential teaching model only; not an atomic database transaction.
    txid = "T" + str(len(receipts) + 1)
    balances[source] -= amount
    balances[target] += amount
    entries.extend([(txid, source, -amount), (txid, target, amount)])
    receipts[scope] = (intent, txid)
    return txid

def snapshot():
    return deepcopy((balances, entries, receipts))

def rejected_without_changes(*args):
    before = snapshot()
    try:
        transfer(*args)
    except (ValueError, PermissionError):
        assert snapshot() == before
    else:
        raise AssertionError("expected rejection")

first = transfer("alice", "A", "B", 3000, "intent-1")
assert balances == {"A": 7000, "B": 5000}
before_retry = snapshot()
assert transfer("alice", "A", "B", 3000, "intent-1") == first
assert snapshot() == before_retry
rejected_without_changes("alice", "A", "B", 3500, "intent-1")
rejected_without_changes("bob", "A", "B", 100, "wrong-owner")
for value in (0, -1, 1.5, True):
    rejected_without_changes("alice", "A", "B", value, "invalid")
rejected_without_changes("alice", "A", "B", 8000, "too-much")
rejected_without_changes("alice", "A", "A", 100, "same-account")
rejected_without_changes("alice", "A", "B", 100, "wrong-currency", "EUR")
assert sum(balances.values()) == 12000
assert sum(entry[2] for entry in entries) == 0
assert len(entries) == 2
print("PASS: ownership, validation, retries and balanced entries")
print(balances)
~~~

Expected: PASS and `{'A': 7000, 'B': 5000}`. Explain why True is rejected even though Python treats bool as a subtype of int. The model rejects it by requiring exactly int.

## Tabletop: overlapping requests

Start with A=100, X=80 and Y=80. Fill the last column:

| Step | Operation | Consequence |
|---|---|---|
| 1 | X reads 100 | X decides it can spend 80 |
| 2 | Y reads 100 | Y makes the same decision |
| 3 | X commits debit and credit | A should now be 20 |
| 4 | Y commits using its stale decision | Explain overspend or lost-update risk |

A transaction alone is not enough unless its isolation/locking and write rules prevent the race. Specify what is locked or serialized, how conflicts retry, and how both ledger sides and idempotency results commit together.

**Design checks, not executed here:** two concurrent requests with the same key; two different keys competing for limited balance; process crash between debit and credit; restart followed by retry; expired or changed approval.

**Save:** actual output, invariants, tabletop result and the list of missing guarantees. Never label the toy “bank-grade.”

[Week 13](../curriculum/WEEK-13.md)

