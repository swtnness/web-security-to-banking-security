# Lab rules and public evidence

This repository is educational. Authorized scope is your local exercise folder and the exact training instance provided to you by Web Security Academy. A public website, your customer account or a login page does not by itself authorize testing.

- Use synthetic names and identifiers such as Alice, Bob and account A-001.
- Use fake balances; do not connect these exercises to real money.
- Keep development servers bound to 127.0.0.1 and stop them after use.
- Do not publish passwords, secret keys, session cookies, reset links, authorization headers, card data or personal information.
- Prefer a small, manually transcribed request with sensitive values removed over a full HAR or proxy export.
- Keep intentionally vulnerable experiments local or inside the assigned training lab.
- Report what you observed and distinguish it from what you merely expect.

Before each public commit: inspect the diff, inspect screenshots, confirm the target was authorized, and replace any live credentials with descriptive placeholders.

If a real secret is committed, revoke or rotate it first. Deleting the current file does not remove it from history. Review the affected service and use GitHub's documented sensitive-data removal process if necessary.

A security concern about this learning material can be recorded privately with the repository owner. Do not open a public issue containing real credentials or customer data.

