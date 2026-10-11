# Module 5 — Evidence and the next learning step

**Week 16.** Your assessment should make a small set of claims that someone else can check.

## Four evidence labels

| Label | Meaning |
|---|---|
| Tested | A specific executed check has a recorded result |
| Partially tested | Evidence covers only part of the claim |
| Planned | A control or test is described but has not been executed |
| Not applicable | A documented scope reason excludes it |

Example: the local transfer function passes sequential retry tests. It does **not** establish concurrency safety, durable recovery or real transaction-approval security.

## Select verification requirements

Use [OWASP ASVS](https://owasp.org/projects/asvs) to choose a small relevant subset for authentication, access control, input/output handling and logging. Record the exact version and requirement identifiers from the document you actually consult. Do not invent IDs, claim an ASVS level, or claim certification from a handful of passing tests.

Build a table: requirement → implementation/location → test → result → limitation. Include at least one failed or incomplete finding with a concrete next step; do not hide gaps.

## What comes after this foundation?

Choose one next project:

1. **Web development:** add framework-based recovery, MFA and rate limiting to the local notes app, with positive and negative tests.
2. **Database integrity:** implement the toy transfer model in a transactional database and test concurrent attempts and crash recovery.
3. **Payments:** integrate a provider's test environment using its official SDK, verify signatures and reconcile synthetic orders.
4. **Operations:** run a controlled backup/restore exercise and test monitoring delivery without using real customer data.

Do one well before expanding scope. Real banking work also involves organizational processes, jurisdiction-specific regulation, privacy, resilience, third-party risk and independent assessment. This learning repository is not a substitute for those.

Finish [the capstone](../05-portfolio-projects/CAPSTONE.md) and update [the tracker](../progress/PROGRESS.md).

