# Web Security → Banking Security | Vannesa's Learning Repository

A **beginner-first, hands-on cybersecurity learning path**, from understanding how websites work to securing banking-like applications. Start at [`00-start-here/START-TODAY.md`](00-start-here/START-TODAY.md). No previous security experience is assumed.

> **Safety:** Only test applications you own, your local development environments, or designated training labs. Never probe actual banking/payment websites without explicit written authorization. Never commit credentials, real payment data, or personally identifiable information.

## Outcomes
- Trace a browser request through DNS, TCP/TLS, HTTP, the web server, and the database.
- Understand common web vulnerabilities and their underlying root causes.
- Reproduce selected vulnerabilities in *authorized training labs*, then explain the mitigations.
- Build and harden a demo application with authentication, authorization, and audit logging.
- Produce a security assessment and threat model for a **simulated** banking system.

## 16-week roadmap (5–7 focused hours per week)

| Week | Focus | Practical output |
|---|---|---|
| 1 | Web architecture, browser DevTools, HTTP/S | Annotated HTTP exchange |
| 2 | Linux shell, files, processes, Git | CLI and Git cheat sheet |
| 3 | HTML, JavaScript, Python basics, cookies | Minimal local web app |
| 4 | Web threat modeling and OWASP Top 10:2025 | Threat model for demo login |
| 5 | SQL injection and input handling | Lab notes and parameterization explanation |
| 6 | XSS, output encoding, CSRF | Lab notes and defensive checklist |
| 7 | Authentication, sessions, access control | Authorized access-control lab report |
| 8 | Secure architecture and code review | Security requirements for demo app |
| 9 | Backend security and database access | Secure CRUD implementation |
| 10 | API security and authorization | API test matrix with negative tests |
| 11 | Security headers, logging, tests, dependency hygiene | Hardened demo with automated tests |
| 12 | Financial threat models and money movement | Simulated transfer data-flow diagram |
| 13 | Transaction authorization, idempotency, race conditions | Transfer invariants and test cases |
| 14 | Payments, PCI DSS concepts, data minimization | Mock payment integration design |
| 15 | Fraud controls, auditability, monitoring, incident response | Monitoring and response playbook |
| 16 | Capstone review and portfolio write-up | Defended mock-banking app assessment |

**Rule:** Advance after you can explain the concept and demonstrate a small artifact, not merely after reading.

## Repository map
- [`00-start-here/`](00-start-here/START-TODAY.md): exact first day and study routine
- [`01-web-foundations/`](01-web-foundations/WEEK-01.md): basic web concepts and first observations
- [`02-web-vulnerabilities/`](02-web-vulnerabilities/LEARNING-LABS.md): sanctioned hands-on security labs
- [`03-defensive-engineering/`](03-defensive-engineering/SECURE-WEB-CHECKLIST.md): how to protect applications
- [`04-banking-security/`](04-banking-security/BANKING-ROADMAP.md): banking-like systems and money movement
- [`05-portfolio-projects/`](05-portfolio-projects/CAPSTONE.md): portfolio deliverables
- [`progress/`](progress/PROGRESS.md): daily evidence and self-evaluation

## Trusted reference material
1. [MDN Web Docs: How the Web works](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Web_standards/How_the_web_works)
2. [MDN HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
3. [PortSwigger Web Security Academy: Getting Started](https://portswigger.net/web-security/getting-started)
4. [PortSwigger Learning Paths](https://portswigger.net/web-security/learning-paths)
5. [OWASP Top 10:2025](https://owasp.org/Top10/2025/)
6. [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
7. [OWASP API Security Top 10:2023](https://owasp.org/API-Security/)
8. [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)
9. [PortSwigger Burp Suite Community Edition](https://portswigger.net/burp/communitydownload)

## Study method
For each topic: **read (20 min) → inspect or build (30 min) → document evidence (10 min)**. Keep terminology, notes, code comments, and reports in technical English. Prefer running all intentionally vulnerable software in an isolated local lab.

## Definition of done
A topic is complete when its notes contain: a definition, a request/response or architecture example, the security impact, a concrete prevention, and evidence from a legal lab (where applicable).
