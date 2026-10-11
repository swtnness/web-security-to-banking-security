# Week 7 — Authentication, sessions and access control

**Prerequisites:** Weeks 4–6: threats, requests and lab evidence.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

Authentication establishes an actor. Authorization decides what that actor can do. An unpredictable record ID can reduce guessing but cannot replace ownership checks. Recovery and logout belong in the identity design.

## Do these sessions in order

1. **Day 1.** Read [Lab 06](../labs/LAB-06-access-control.md). Build a matrix for guest, Alice, Bob and support staff against read/edit/delete actions.

2. **Day 2.** Complete the named Academy access-control exercise. Record the difference between a hidden interface element and an enforced server decision.

3. **Day 3.** Walk through login → session creation → request → logout. Write where a framework validates credentials and resolves the session.

4. **Day 4.** Design recovery for the fictional user. Consider generic responses, single-use expiring tokens, rate limits, user notifications and invalidating relevant sessions.

5. **Day 5.** Add session-expiry and direct-URL cases to the matrix. Identify which tests should still fail after an attacker changes an object identifier.

6. **Day 6.** Write a report and a ten-line policy: default deny, per-object checks, least privilege and no trust in a client-supplied role.

## Evidence

Save `progress/lab-06-report.md` and the access matrix. Label recovery and session cases as planned until implemented.

## Checkpoint

Can you explain why a signed-in user may still be denied and why removing an admin button does not protect an endpoint?

Reading: [OWASP authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) and [authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html).

[Previous](WEEK-06.md) · [Next](WEEK-08.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

