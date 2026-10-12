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

## My Lab Results — Vannesa

**Date:** 2026-10-11  
**Week:** 1  
**Lab:** 01 — Observe an HTTP Request  
**Target:** https://example.com/  
**Tools:** Google Chrome Developer Tools — Network tab  
**Time spent:** [Enter actual minutes]

### Goal
Understand how a browser communicates with a web server by inspecting a real HTTP request and response.

### Actions Performed
1. Opened example.com in Google Chrome.
2. Opened Developer Tools and selected the Network tab.
3. Inspected the main document request.
4. Identified the request URL, HTTP method, status code, and response headers.
5. Investigated the meaning of the 304 Not Modified response.

### Expected Result
I expected the browser to send a GET request and receive an HTTP response containing the webpage, possibly with a 200 OK status.

### Actual Result
- Request URL: https://example.com/
- Request Method: GET
- Status Code: 304 Not Modified
- Remote Address: 172.66.147.243:443
- Response Header 1: Age: 9015
- Response Header 2: Allow: GET, HEAD
- Additional Header: Cf-Cache-Status: HIT

The server returned a 304 Not Modified response rather than a 200 OK response. This indicated that a previously cached representation could be reused.

### Client vs. Server
- Client: The browser initiated the HTTP GET request.
- Server: The remote endpoint responded with an HTTP status code and response headers.
- Browser: The browser can reuse cached content after successful cache validation.

### Explanation — In My Own Words
When I opened example.com, my browser sent an HTTP GET request to retrieve the webpage. I observed a 304 Not Modified status instead of a 200 OK response. This means the browser could reuse a previously stored version of the resource. The response headers also provided information about caching and supported HTTP methods. I learned that successful HTTP communication does not always require downloading the complete webpage again.

### Security Perspective
HTTPS protects data transmitted between the browser and the remote server. HTTP caching improves performance, but sensitive information requires appropriate cache-control policies. A successful HTTP response does not guarantee that a web application is completely secure.

### Evidence
Chrome Developer Tools screenshot — to be saved as `labs/day-01-http-exchange.png`.

### Pending Verification
Inspect the Response or Preview tab and compare the available content with the visible webpage.

### Blocker / Question
What is the difference between browser caching and CDN caching?

### Next Action
Complete the Response/Preview inspection, then study HTTP methods, URLs, status codes, and request headers.

### Help Used
Walkthrough — ChatGPT cybersecurity mentoring.

