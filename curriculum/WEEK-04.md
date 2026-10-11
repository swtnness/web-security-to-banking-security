# Week 4 — Threat modeling before testing

**Prerequisites:** Weeks 1–3: browser/server roles, HTTP and basic code.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

A threat model starts with what you are protecting. An asset can be a private note, a session or an account balance. A threat describes how it could be exposed, changed or made unavailable. A control reduces a specific threat; it needs evidence.

## Do these sessions in order

1. **Day 1.** Read [Lab 03](../labs/LAB-03-threat-model.md). Define the notes app's purpose, users and data. Mark all names and examples as synthetic.

2. **Day 2.** Draw browser → web app → database, with an authentication/session component. Mark the public browser boundary and database access boundary.

3. **Day 3.** Create five abuse cases, including reading another person's note, changing ownership, executable text, stolen session and service overload. Describe harm without assuming exploitation succeeded.

4. **Day 4.** For each case, record a preventive control, a detection idea and a test. Place the control at the component that can enforce it.

5. **Day 5.** Read the current [OWASP Top 10](https://owasp.org/Top10/) overview as a risk map. Then open ASVS and distinguish awareness material from testable requirements. Record the version you consulted.

6. **Day 6.** Review your scope and top three priorities. Explain why hiding a button and adding HTTPS cannot fix a missing ownership check.

## Evidence

Save `progress/week-04.md` using the threat-model template, with a diagram and at least five threat/control/test rows.

## Checkpoint

Can another person identify the asset, boundary and test for each priority? Rewrite any row that only says 'use better security'.

Reading: [OWASP ASVS](https://owasp.org/projects/asvs).

[Previous](WEEK-03.md) · [Next](WEEK-05.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

