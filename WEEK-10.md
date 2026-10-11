# Week 10 — API authorization and regression tests

**Prerequisites:** Week 9 working local notes app.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

An API exposes the same data through a different interface. JSON is not a permission boundary. Tests must check both the allowed operation and the denied case, including that denied writes leave data unchanged.

## Do these sessions in order

1. **Day 1.** Read [Lab 08](../labs/LAB-08-api-tests.md). Add the read-only note API. Describe its data contract and session-based authentication behavior.

2. **Day 2.** Inspect the API as Alice, Bob and a guest. Record status and fields for each; do not assume browser redirects mean JSON clients received a useful error.

3. **Day 3.** Add the supplied automated tests. Explain setUp, force_login, assertions and why the test database is separate.

4. **Day 4.** Run the test suite. Confirm the cross-user read/edit/delete tests and owner-spoofing test pass. Read a failure from bottom to top if something breaks.

5. **Day 5.** Run the CSRF tests with enforce_csrf_checks enabled. Confirm that a valid token permits creation and missing or incorrect tokens reject it.

6. **Day 6.** Add one new test: change a note body to empty text or request a nonexistent identifier. Record expected and actual outcomes and the protected property.

## Evidence

Save `progress/lab-08-report.md` with test command, actual result, date and your new case.

## Checkpoint

Can you show a passing authorized case and a failing unauthorized case for the same object? Explain why a 404 alone does not prove a delete had no side effect.

Reading: [Django test tools](https://docs.djangoproject.com/en/5.2/topics/testing/tools/).

[Previous](WEEK-09.md) · [Next](WEEK-11.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

