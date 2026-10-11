# Lab 04 — SQL input and parameterization

**Week:** 5. **Target:** your assigned Academy instance and an in-memory local database. **Time:** two or three sessions.

## Hosted training

Open [SQL injection in a WHERE clause](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data). Launch your own lab instance and use only that instance. Observe the category filter's normal request before changing it. The training objective is to reveal the lab's hidden products.

Hint: identify where the category value becomes part of a database condition. Work for 20 minutes before using the platform's solution. Record exactly how much help you used. Do not apply the experiment to shops or bank sites.

## Local defensive exercise

Save this as `exercises/sql/parameters.py`. Create the folder first. Run `python parameters.py` there.

~~~python
import sqlite3

db = sqlite3.connect(":memory:")
db.execute("CREATE TABLE products (name TEXT, category TEXT, released INTEGER)")
db.executemany("INSERT INTO products VALUES (?, ?, ?)", [
    ("Practice notebook", "Books", 1),
    ("Unreleased guide", "Books", 0),
    ("Toy mug", "Home", 1),
])

def visible_products(category):
    return db.execute(
        "SELECT name FROM products WHERE category = ? AND released = 1",
        (category,),
    ).fetchall()

assert visible_products("Books") == [("Practice notebook",)]
assert visible_products("Books' OR 1=1 --") == []
assert visible_products("Missing") == []
print("PASS: normal, SQL-looking and missing categories")
db.close()
~~~

Expected: the PASS line. The SQL-looking string is a test value, not part of the SQL grammar. Explain the question mark and the separate one-item tuple.

## Reflect

- What changed between ordinary data and executable query structure in the vulnerable training app?
- Why is banning apostrophes harmful to legitimate names and insufficient as a primary defense?
- What would prevent Alice from querying Bob's authorized-but-private data?

[OWASP's SQL prevention guidance](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html) supports query parameterization and limited database privileges. Parameterization does not establish ownership; that is a separate rule.

Save the actual local output and a [lab report](../templates/LAB-REPORT.md). If the hosted lab is unavailable, complete the local part and mark the hosted observation pending rather than solved.

[Week 5](../curriculum/WEEK-05.md)

