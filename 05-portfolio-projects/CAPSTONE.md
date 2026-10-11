# Portfolio and Week 16 capstone

Build evidence progressively. You do not need a new production banking application to complete this curriculum.

## Four portfolio artifacts

1. **HTTP field notes, Week 1:** one observed request, a flow diagram and your explanation of HTTPS.
2. **Security lab reports, Weeks 4–7:** the threat model and SQL, browser-security and access-control reports. State where platform hints were used.
3. **Protected notes website, Weeks 8–11:** local app source, setup instructions, authorization/CSRF tests, configuration review and residual risks.
4. **MiniBank assessment, Weeks 12–16:** financial threat model, transfer and event simulation results, concurrency/approval design and incident playbook.

Put a portfolio index in `progress/portfolio-index.md` as you complete these items. Link actual artifacts; do not link empty “completed” reports.

## Final assessment structure

Use [the assessment template](../templates/ASSESSMENT.md). Include:

- A short description of what you built and studied.
- Exact scope: local notes app, synthetic finance models and assigned training labs.
- Architecture diagrams and trust boundaries.
- Requirements and a threat-to-control mapping.
- Test table with expected result, actual result, evidence and date.
- At least three findings or limitations, with impact and a proposed or completed fix.
- Explicit residual risks and the next step you would take.

A finding can be a missing control in the learning app, such as absent MFA or login throttling. Do not fabricate an exploited vulnerability.

## Acceptance criteria

- [ ] The README and your portfolio index open the actual evidence.
- [ ] You explain one request in your own words.
- [ ] Three vulnerability reports connect root cause to prevention and a retest.
- [ ] Your local app demonstrates owned CRUD and denial of cross-user requests.
- [ ] Your test suite includes authorized and unauthorized paths, CSRF, validation and logout.
- [ ] Financial tests demonstrate sequential retry behavior and event deduplication.
- [ ] You explain why concurrency, durable processing and approval cryptography remain unimplemented.
- [ ] The incident exercise separates facts, hypotheses and unknowns.
- [ ] No live secrets, payment data or private captures are published.
- [ ] You can give a five-minute demonstration and explain its limits.

## Five-minute demonstration

Spend one minute each on the HTTP request, a vulnerability and defense, the notes-app tests, the financial simulations, and your most important unresolved risk.

## Self-review rubric

Score each area 0–2: explanation, reproducibility, evidence, defensive reasoning, honesty about limits. 0 = missing; 1 = partial; 2 = clear. Aim for at least 8/10 and resolve any zero before presenting the work. This is a course self-check, not an industry certification.

[Week 16](../curriculum/WEEK-16.md) · [Progress](../progress/PROGRESS.md)

