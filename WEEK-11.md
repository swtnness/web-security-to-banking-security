# Week 11 — Hardening, logs and maintenance

**Prerequisites:** Week 10 tests pass; the app remains local.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

Security depends on configuration and operation as well as code. Debug pages, leaked secrets, stale dependencies and missing logs can undermine good authorization. A scanner result is an input to review, not a guarantee.

## Do these sessions in order

1. **Day 1.** Complete [Lab 09](../labs/LAB-09-hardening.md) part A. Inspect local response headers and cookie attributes; record what is present rather than guessing.

2. **Day 2.** Add the narrow synthetic audit logging in part B. Trigger an allowed update and an ownership denial. Verify logs contain no body text, password or session token.

3. **Day 3.** Run the framework's deployment check in part C. Classify each warning as a local-development exception or a future deployment requirement.

4. **Day 4.** Record installed package versions and read the framework's release/security guidance. Write a repeatable update → test → review process.

5. **Day 5.** Use the defensive checklist to mark tested, planned and not applicable controls. Plan HTTPS cookies, a secret store, rate limiting and restore testing; do not enable settings blindly on local HTTP.

6. **Day 6.** Re-run the regression suite and review the public diff. Write the three most important remaining risks before showing this app in a portfolio.

## Evidence

Save `progress/lab-09-report.md` with configuration observations, sanitized log examples, test output and deployment limitations.

## Checkpoint

Can you distinguish a local demo exception from an acceptable production setting and prove no sensitive text entered the sample logs?

Reading: [Django deployment checklist](https://docs.djangoproject.com/en/5.2/howto/deployment/checklist/) and [OWASP logging](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html).

[Previous](WEEK-10.md) · [Next](WEEK-12.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

