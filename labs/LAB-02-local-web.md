# Lab 02 — A local page and small Python decisions

**Weeks:** 1 part A; 3 parts B–C. **Target:** your own local files. **Time:** three sessions.

## A. Create the page

Create `exercises/static-site/` inside your learning repository. Save the following as `index.html` in that folder. In Notepad choose All files, UTF-8; do not save index.html.txt.

~~~html
<!doctype html>
<html lang="en">
<meta charset="utf-8">
<title>Vannesa's web lab</title>
<h1>My first web lab</h1>
<form id="greeting">
  <label>Fake display name <input id="name" maxlength="40" required></label>
  <button>Say hello</button>
</form>
<p id="result"></p>
<script>
const form = document.querySelector("#greeting");
const nameInput = document.querySelector("#name");
const result = document.querySelector("#result");
form.addEventListener("submit", (event) => {
  event.preventDefault();
  result.textContent = "Hello, " + nameInput.value;
});
</script>
</html>
~~~

Open it by double-clicking. Try Alice, empty input and `<b>Alice</b>`. Expected: a greeting, a browser validation prompt for empty input, and literal angle-bracket text. No network account is created. This form intentionally has no backend.

## B. Serve it locally in Week 3

Open PowerShell **inside exercises/static-site**, then run:

~~~powershell
python -m http.server 8000 --bind 127.0.0.1
~~~

Visit `http://127.0.0.1:8000/index.html`. Inspect the main request as in Lab 01. Request `http://127.0.0.1:8000/missing.html` and observe a 404. Stop the server with Ctrl+C.

Only serve this synthetic exercise folder, not your whole repository or Documents folder. This server is for local learning; [Python documents its limited security](https://docs.python.org/3/library/http.server.html).

## C. Read and run Python

Create `exercises/python-basics/`. Save this as `ownership.py` and run `python ownership.py` from that folder:

~~~python
record = {"id": 1, "owner": "alice", "body": "Practice note"}
actors = ["alice", "bob", None]

def can_read(actor, note):
    if actor is None:
        return False
    return actor == note["owner"]

for actor in actors:
    print(actor, can_read(actor, record))
~~~

Expected:

~~~text
alice True
bob False
None False
~~~

A dictionary maps keys to values; the list supplies inputs; the function returns a decision; the loop repeats the check. This function is a model of a rule, not a login system. A real app must derive the actor from a verified server-side session.

**Change:** add an `archived` field and deny reads when it is True. Try all actors with archived False and True. Explain the condition in plain English.

**Save:** the code, observed outputs and why changing a browser-side owner value must not change a server's authorization decision.

[Week 3](../curriculum/WEEK-03.md)

