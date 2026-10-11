# Lab 05 — Separate XSS from CSRF

**Week:** 6. **Target:** assigned Academy lab, your own local page and a fictional request. **Time:** two or three sessions.

## A. Untrusted content as code

Launch [reflected XSS in an HTML context](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded). Identify the input and the place it is reflected. Complete only the platform's demonstration goal and record its result.

Return to Lab 02. Enter `<b>Alice</b>`; textContent displays it literally. Explain why choosing a text API avoids treating this value as HTML. Do not change this page into a credential-collection or data-exfiltration exercise.

Expected evidence: one platform observation and one local literal-text result. They are different implementations, so the local result does not prove the hosted application was fixed.

## B. A fictional unwanted request

A notes app accepts POST /notes/1/delete/. The browser automatically attaches its session cookie. A different site attempts to make the browser submit that action without Alice's intent.

Trace: external page → browser request → attached cookie → server action. The server must still check ownership, request method and its CSRF protection. A valid login alone is not sufficient.

Fill this matrix now; execute equivalent cases in Lab 08 later:

| Request | Intended outcome in our notes app |
|---|---|
| Alice, owned object, valid CSRF token, POST | Delete one owned object |
| Alice, owned object, missing token, POST | 403; object remains |
| Bob, Alice's object, valid token, POST | 404; object remains |
| Alice, owned object, GET | 405; object remains |

## Defenses to explain

Use safe text rendering or context-appropriate escaping for XSS. Use the framework's CSRF mechanisms for browser requests carrying cookies; combine these with appropriate SameSite settings and origin validation. Neither control replaces object authorization. CSP provides another browser layer but is not a substitute for safe output handling.

References: [OWASP XSS prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html) and [OWASP CSRF prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html).

**Save:** a report with separate cause, impact, prevention and verification sections for XSS and CSRF.

[Week 6](../curriculum/WEEK-06.md)

