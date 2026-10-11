# Lab 06 — Who may do what?

**Week:** 7. **Target:** assigned training instance and fictional notes app. **Time:** two sessions.

## Prepare the policy

| Actor | Read Alice's note | Edit Alice's note | Read Bob's note |
|---|---|---|---|
| Guest | Deny | Deny | Deny |
| Alice | Allow | Allow | Deny |
| Bob | Deny | Deny | Allow |
| Support employee without special approval | Deny | Deny | Deny |

An administrator role needs a separately justified policy; do not give every support employee unrestricted data access.

## Hosted practice

Launch [unprotected admin functionality](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality). Work only inside the disposable lab instance. Follow its stated objective, which concerns synthetic accounts within that instance.

1. Observe the ordinary site and its available navigation.
2. Determine whether the training admin action has a server-side access check.
3. Record the difference between finding an endpoint and being authorized to use it.
4. Describe a deny-by-default server control and a test for an ordinary user.

Record the observed result without publishing a live lab cookie. If a platform solution was used, say so.

## Defensive design exercise

For each notes-app endpoint, write the verified actor, requested action, target object, ownership query and denial result. Include direct URLs, not just navigation buttons. Then add logout and expired-session cases.

Expected result: changing the object identifier does not change who the requester is. Session expiry denies access. A missing object and an inaccessible object can both use 404 in this app to avoid revealing existence.

## Recovery review

Write a short fictional password-reset flow. Include a generic initial response, a short-lived single-use token, protected delivery, throttling and notification. Record how session revocation would be handled. You are designing this flow; the later notes app does not implement email recovery or MFA.

Sources: [OWASP authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html), [OWASP authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html).

[Week 7](../curriculum/WEEK-07.md)

