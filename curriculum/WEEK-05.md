# Week 5 — SQL injection and safer database queries

**Prerequisites:** Week 3 Python and Week 4 scope. Install Burp only if using the hosted lab.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

SQL injection happens when input changes a query's structure. A parameterized query supplies values separately. Validation also matters, but a rule that blocks quotes is not a substitute for parameters.

## Do these sessions in order

1. **Day 1.** Read [Lab 04](../labs/LAB-04-sql.md). Identify table, row, column, SELECT and WHERE in the toy query. Write its normal expected result.

2. **Day 2.** Launch the named Academy SQL lab and inspect one normal category-filter request. Record the allowed target and changed parameter without copying session cookies.

3. **Day 3.** Attempt the assigned training goal. Use the hint after 20 focused minutes if needed. Record whether you solved it independently, with a hint, or by following the solution.

4. **Day 4.** Run the local SQLite prevention exercise. Compare a normal category and a value containing SQL-looking text. Explain why the second remains data.

5. **Day 5.** Write two regression cases and one least-privilege improvement. Explain why successful parameterization does not establish object authorization.

6. **Day 6.** Write a report using the lab template. Re-run the local assertions and explain the fix without reading the source.

## Evidence

Save `progress/lab-04-report.md`: baseline, training observation, local defensive output and two regression cases.

## Checkpoint

Can you identify where untrusted data would enter a query and show it passed as a separate value? Revisit the local snippet if not.

Reading: [OWASP SQL injection prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).

[Previous](WEEK-04.md) · [Next](WEEK-06.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

