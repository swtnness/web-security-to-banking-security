# Week 8 — Design a small protected web app

**Prerequisites:** Weeks 1–7 and working Python. Review functions and dictionaries if needed.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

Your project is deliberately small: private notes owned by fake users. Framework authentication, form handling and database access let you focus on policy. The framework does not decide record ownership for you.

## Do these sessions in order

1. **Day 1.** Read [Lab 07](../labs/LAB-07-protected-notes.md) and [the defensive checklist](../03-defensive-engineering/SECURE-WEB-CHECKLIST.md). Write five requirements for the notes app.

2. **Day 2.** Complete Lab 07 steps 1–2: create the environment and project and replace the generated development secret setting. Record your Python and Django versions.

3. **Day 3.** Complete step 3's model and form. Draw User 1 → many Notes. Explain why owner is absent from the browser-editable form fields.

4. **Day 4.** Trace the views and routes in step 4 on paper before copying. Identify the login gate, ownership query, method restriction and server-chosen owner.

5. **Day 5.** Make a review checklist with one negative test per requirement. Add a threat about someone assigning a note to a different owner.

6. **Day 6.** Review the app plan against your Week 4 threat model. Commit only the starter source and notes after checking for generated secrets or database files.

## Evidence

Save `progress/week-08.md` with requirements, model diagram, versions and a review checklist. Lab 07 is finished next week.

## Checkpoint

Can you point to the place where each of your five requirements will be enforced? Do not claim a control is tested yet.

Reading: [Django 5.2 introduction](https://docs.djangoproject.com/en/5.2/intro/tutorial01/).

[Previous](WEEK-07.md) · [Next](WEEK-09.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

