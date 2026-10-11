# Week 9 — Implement protected records and database access

**Prerequisites:** Week 8 project skeleton and security requirements.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

CRUD means create, read, update and delete. All four operations need ownership rules. A successful login is only the beginning of request processing; every object lookup needs the current actor's policy.

## Do these sessions in order

1. **Day 1.** Finish Lab 07 step 4 views and routes. Trace a request from URL to ownership-filtered query to response.

2. **Day 2.** Add the templates in step 5. Find the CSRF token in every changing form and the automatically escaped note body.

3. **Day 3.** Run migrations and create the two fake users in step 6. Start the server on 127.0.0.1. Create, view and edit a note as Alice.

4. **Day 4.** Open a second private-browser session as Bob. Try Alice's note detail, edit and delete URLs. Confirm a denial and verify Alice's record still exists.

5. **Day 5.** Test blank content, markup-looking content and deletion with GET. Inspect actual responses; expected outcomes are in Lab 07.

6. **Day 6.** Write a short code review. Highlight the server-selected owner, ORM parameters, form validation and escaped template. Save only fake data and sanitized evidence.

## Evidence

Save `progress/lab-07-report.md` and your completed local notes-app source under `exercises/notes-app/`.

## Checkpoint

Can Alice do all four CRUD operations on her notes while Bob cannot read, change or delete them? Fix failures before Week 10.

Reading: [Django authentication](https://docs.djangoproject.com/en/5.2/topics/auth/default/).

[Previous](WEEK-08.md) · [Next](WEEK-10.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

