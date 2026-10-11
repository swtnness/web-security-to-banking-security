# Financial application security — simulated systems

Start this stage after the web-development and authorization checkpoints. The system is **MiniBank**, a fictional service with synthetic accounts and fake USD balances. There is no real bank connection, payment processing or identity-document collection.

| Module | Week | Focus | Evidence |
|---|---|---|---|
| [1 — Assets and boundaries](01-threat-model.md) | 12 | Account ownership, identity and trust | Diagram and threat register |
| [2 — Money movement](02-money-movement.md) | 13 | Approval, invariants, atomicity and retries | Transfer simulation and concurrency plan |
| [3 — Payments and data](03-payments-and-data.md) | 14 | Hosted checkout, webhooks and minimization | Event tests and data-flow design |
| [4 — Monitoring and response](04-monitoring-and-response.md) | 15 | Detection, investigation and recovery | Tabletop playbook |
| [5 — Assurance and next steps](05-assurance.md) | 16 | Evidence, scope and further study | Final assessment |

## Prerequisite check

- [ ] I can distinguish authentication, authorization and transaction approval.
- [ ] I can demonstrate a denied cross-user request.
- [ ] I can explain server-side validation and parameterized data access.
- [ ] I can run and interpret a small automated test.
- [ ] I can distinguish observed results from assumptions.

## What this stage does and does not implement

The Python transfer exercise tests sequential in-memory decisions. The event exercise tests business validation and deduplication. Transaction approval, database concurrency, cryptographic webhook verification, operational resilience and regulatory obligations are design topics here, with concrete test plans. Do not present them as implemented.

A protected learning application is not a certified banking system. Real deployments need domain specialists, legal/compliance review appropriate to jurisdiction, independent security review and operational controls.

[Full curriculum](../curriculum/ROADMAP.md) · [Capstone](../05-portfolio-projects/CAPSTONE.md)

