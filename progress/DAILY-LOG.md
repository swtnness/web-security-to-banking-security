# Daily study journal
## Entry 1

Date: 2026-10-11
Week / day: Week 1 / Day 1
Minutes studied: 60
Topic and resource: How the Web Works — MDN

- Goal: Understand the basic flow of how the web works, including DNS, TCP, TLS, HTTP, and browser rendering.
- Action: I read the MDN article "How the Web Works", reviewed the explanation with ChatGPT, and answered a short exercise in my own words.
- Expected result: I expected to understand what happens when I type a website address into a browser and press Enter.
- Actual result: I understood the general sequence: DNS resolves the domain to an IP address, the browser establishes a TCP connection, TLS protects the connection, the browser sends an HTTP request, the server returns a response, and the browser renders the page. I also learned that I confused who sends and receives the HTTP request at first.
- Evidence: notes/lesson-01-how-the-web-works.md
- Explanation: In my own words, when I enter a website address, the browser first finds the server IP using DNS. Then it creates a connection, usually protected with TLS if the site uses HTTPS. After that, the browser sends an HTTP request, the server sends back the response, and the browser shows the content. A successful connection does not automatically mean the web application is secure.
- Defense: Security controls belong mainly on the server side. The server must validate requests, verify authentication and authorization, and protect data in transit with HTTPS/TLS. I can check part of this in the browser using Developer Tools and the Network tab.
- Blocker / question: I still need to understand more clearly the difference between TCP, TLS, and HTTP, and why HTTPS does not mean the application is fully secure.
- Next action: Review HTTP requests and responses in the browser Network tab and study HTTP methods, headers, cookies, and sessions.
- Help used: walkthrough

## Week 1 — Day 2: URLs and HTTP Communication

**Date:** 2026-10-14  
**Week / Day:** Week 1 / Day 2  
**Minutes studied:** [Enter actual minutes]  
**Topic and resource:** URL Anatomy, HTTP Methods, HTTP Status Codes — MDN HTTP Overview

### Goal
Understand how URLs identify web resources and how HTTP clients and servers communicate using requests, responses, headers, and status codes.

### Action
- Studied HTTP fundamentals and URL structure.
- Completed three written questions about GET vs POST, HTTP 403, and URL fragments.
- Passed a correction quiz.
- Identified the six components of an example URL.
- Constructed an illustrative HTTP/1.1 GET request and response with two headers each.

### Expected Result
I expected to understand URL components and independently construct a basic HTTP request and response.

### Actual Result
I successfully identified the scheme, hostname, port, path, query, and fragment.

I constructed a correctly structured GET request and a successful HTTP response. I made a spelling error in the Content-Length header and corrected it.

I also learned that POST requests may contain URL query parameters, HTTP 403 does not necessarily prove successful authentication, and fragments are normally handled by the browser.

### Evidence
- Handwritten HTTP questions and corrections.
- Completed URL anatomy exercise.
- Illustrative HTTP request and response.
- [Add a relative link to the saved Day 2 notes.]

### Explanation
A URL identifies a resource and contains components such as a scheme, hostname, path, and optional parameters. An HTTP client sends a request containing a method and headers. The server processes the request and sends an HTTP response with a status code, headers, and possibly a response body.

### Defense
HTTPS protects HTTP communication in transit. Servers must enforce authentication, authorization, and input validation. A successful HTTP response does not guarantee that the application is secure.

### Blocker / Question
I want to understand how HTTP request bodies differ from URL query parameters.

### Next Action
Study and draw the DNS, TCP, TLS, and HTTP communication flow for Day 3.

### Help Used
Walkthrough — ChatGPT cybersecurity mentoring.

## Entry template

**Date:** YYYY-MM-DD  
**Week / day:**  
**Minutes studied:**  
**Topic and resource:**  

- **Goal:** what I intended to learn or test.
- **Action:** what I read, built or inspected.
- **Expected result:** what I thought would happen.
- **Actual result:** what happened, including errors.
- **Evidence:** relative link to a sanitized report, code file or image I created.
- **Explanation:** the concept in my own words.
- **Defense:** where the protection belongs and how to check it.
- **Blocker / question:** one specific uncertainty.
- **Next action:** a small next step.
- **Help used:** none, hint or walkthrough.

Before publishing, inspect all pasted text and images for secrets and private information. A failed experiment with an honest explanation is useful evidence.

