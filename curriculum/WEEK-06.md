# Week 6 — XSS, browser trust and CSRF

**Prerequisites:** Week 3 forms and JavaScript; Week 5 lab-report routine.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

XSS involves the browser interpreting untrusted content as code. CSRF involves a browser sending an unwanted authenticated action. They need different protections. A login cookie does not prove the user intended every request.

## Do these sessions in order

1. **Day 1.** Read [Lab 05](../labs/LAB-05-browser-security.md). Draw where user text enters and where the page displays it.

2. **Day 2.** Use the named Academy reflected-XSS exercise. Record the training-only result and the output context. Do not collect cookies or data.

3. **Day 3.** Repeat Lab 02's markup input using textContent. Explain the difference between rendering text and inserting HTML. Identify where a framework's default escaping helps.

4. **Day 4.** Trace the fictional CSRF case in Lab 05. List the request's credentials, missing intent proof and server-side checks.

5. **Day 5.** Fill in the CSRF test matrix. Distinguish a planned defense from an executed test; you will execute the Django token tests in Week 10.

6. **Day 6.** Write one report with separate XSS and CSRF sections. Explain why CSP is an additional layer and why SameSite alone is not your entire CSRF strategy.

## Evidence

Save `progress/lab-05-report.md` with a local text-rendering result and four CSRF expected outcomes.

## Checkpoint

Given unwanted script execution versus unwanted form submission, can you select the right primary control and justify it?

Reading: [OWASP XSS prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html) and [CSRF prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html).

[Previous](WEEK-05.md) · [Next](WEEK-07.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

