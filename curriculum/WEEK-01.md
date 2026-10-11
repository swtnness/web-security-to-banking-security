# Week 1 — Your first seven days

**Prerequisites:** none. **Time:** about 6 hours. **Goal:** understand a normal web request before studying attacks. Use [Setup](../00-start-here/SETUP.md) only when a task needs it.

## Day 1 — Watch one page load · 60 minutes

- 5 min: create a journal entry.
- 15 min: read [MDN: how the web works](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Web_standards/How_the_web_works).
- 25 min: complete [Lab 01](../labs/LAB-01-http.md).
- 15 min: record the request method, response status and two nonsensitive headers.

**Save:** five sentences in your journal and one sanitized observation. **Check:** which message did your browser send?

## Day 2 — Read a URL and an HTTP exchange · 60 minutes

- 15 min: read the introduction to [MDN's HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview).
- 20 min: split `https://example.com:443/notes?page=2#top` into scheme, hostname, port, path, query and fragment. This is an example to annotate, not a target to test.
- 15 min: write the meanings of GET, POST, 200, 302, 401, 403 and 404.
- 10 min: sketch a request line, two headers and a response. Mark this sketch as illustrative.

**Save:** ten terms with short definitions. **Check:** the fragment `#top` is handled by the browser and is not included in an ordinary HTTP request target. A POST is not inherently authenticated or encrypted.

## Day 3 — Follow the connection · 60 minutes

- 15 min: read the DNS, IP and TLS glossary entries and revisit MDN's request explanation.
- 20 min: draw browser → DNS lookup → connection and TLS → HTTP request → server response → rendered page.
- 15 min: mark the browser, network, application and database. Not every page needs a database.
- 10 min: write two protections TLS provides and two problems it does not fix.

**Save:** a text diagram is enough. **Check:** TLS protects data in transit and authenticates the server for its name when validation succeeds; it does not prove a site's business is honest or fix broken authorization. The simple TCP sequence describes HTTP/1.1 and HTTP/2; HTTP/3 uses QUIC.

## Day 4 — Make a page · 60 minutes

- 10 min: open Notepad or another text editor.
- 30 min: complete **part A only** of [Lab 02](../labs/LAB-02-local-web.md). Save index.html and open it locally.
- 10 min: change the heading and try a fake name in the form.
- 10 min: explain which elements came from HTML and what JavaScript changed.

**Save:** your page under `exercises/static-site/` and a short note. **Check:** no server account or session exists just because the page says hello.

## Day 5 — Cookies and signed-in state · 60 minutes

- 15 min: read the cookie, session, authentication and authorization glossary entries.
- 20 min: draw a fictional login: credentials → server verification → session cookie → later request.
- 15 min: annotate Secure, HttpOnly and SameSite. Secure restricts transmission to secure contexts under browser rules; HttpOnly blocks direct JavaScript cookie access; SameSite affects cross-site sending.
- 10 min: explain why deleting or changing a visible account ID does not authorize access to a different account.

**Save:** the diagram plus two examples: “Alice signs in” and “Alice may read her own note.” **Check:** identify which is authentication and which is authorization. Do not inspect or publish your real banking session.

## Day 6 — Organize and save evidence · 45 minutes

- 15 min: review your notes and remove private data. A transcribed header is fine; an unreviewed HAR export is not.
- 15 min: add the notes to `progress/DAILY-LOG.md` using a text editor or GitHub's pencil button.
- 15 min: update the [week-one tracker](../progress/PROGRESS.md). Read the setup's Git section if time remains; terminal Git practice is Week 2.

**Save:** one reviewed Markdown update. **Check:** can you reopen it and follow its links?

## Day 7 — Review or catch up · 15–30 minutes

Answer without notes:

1. What does DNS help a browser find?
2. Which side sends an HTTP response?
3. What do a status code and a response body tell you?
4. What does HTTPS protect, and what does it not prove?
5. Why cannot a browser-only check enforce account ownership?

**Self-check:** hostname records such as IP addresses; the server; processing outcome and returned content; transit protection, not application correctness; clients can be changed and the server must enforce policy.

**Pass:** explain at least four correctly, then repair the missing explanation. Keep the local page and one real request observation. If the practical task failed, repeat it before moving on.

[Next: Week 2](WEEK-02.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

