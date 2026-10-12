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

