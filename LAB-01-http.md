# Lab 01 — Observe an HTTP request

**Week:** 1. **Time:** 25–40 minutes. **Target:** normal browsing of [example.com](https://example.com), a documentation example page. **Tools:** browser only.

## Do

1. Open the page, then Developer Tools → Network. Clear the list if it contains older requests.
2. Reload the page. Select the main document request, often named example.com or “/”.
3. In Headers, find the request URL and method. Find the response status and two response headers such as content-type and cache-control. Names and values vary; record your observation.
4. Look at Response or Preview. Match the returned content to the visible page.
5. Record which fields came from your browser and which came from the server.
6. Close Developer Tools after writing your note. Do not export the full browsing session.

## Expected result

You can identify one document request and its response. A successful fresh load commonly returns 200; a cached response, redirect or connection error is still evidence to explain. If the list is empty, check recording is enabled and reload with Developer Tools open. Use “Disable cache” while DevTools is open if you want a fresh request.

## Save

In your daily log: date, target, method, actual status, two nonsensitive response headers, and a five-sentence explanation. Crop out unrelated tabs and account details if using a screenshot.

**Defensive lesson:** understand the ordinary exchange before deciding what a suspicious one means. A successful response is not evidence that every security control works.

**Check:** what happens to the response body after the browser receives it?

[Return to Week 1](../curriculum/WEEK-01.md)

