# Setup, only when you need it

Use Windows PowerShell commands below. Do not paste the Markdown fence lines into a terminal. A command runs when you press Enter. Stop a development server with **Ctrl+C**.

## Week 1: browser and notes

Use an updated Edge, Chrome or Firefox browser. Open Developer Tools with F12 or Ctrl+Shift+I. If function keys control your laptop volume, use the browser menu → More tools → Developer tools.

A plain text editor is enough. In Notepad, use **Save as → All files**, UTF-8, and the exact filename. Turn on **File Explorer → View → Show → File name extensions** to spot accidental `.md.txt` and `.html.txt` files.

Your repository is the folder containing README.md. Course notes go under `progress/`. Screenshots may go under `progress/evidence/`; crop and redact before adding them. A text transcript is acceptable.

## Week 2: Git

Install [Git for Windows](https://git-scm.com/downloads/win) if `git --version` fails. Reopen PowerShell after installing. Git saves snapshots locally; GitHub hosts a copy online.

For the real repository, clone it once into a NEW empty location:

~~~powershell
git clone https://github.com/swtnness/web-security-to-banking-security.git
cd web-security-to-banking-security
git status
~~~

Do not run `git init` inside an existing clone. The upload guide offers a browser-only route. If Git requests identity, use your chosen display name and your GitHub-provided no-reply address from email settings. Never type a password or token into a command you will publish.

Daily work: edit → inspect `git diff` → stage only reviewed files → commit → push when ready. Use `git add progress/DAILY-LOG.md` for a specific file. A commit message such as `Add week 1 HTTP notes` explains the change.

## Week 3: Python

Install a supported Python 3 release from [python.org](https://www.python.org/downloads/); Python 3.12 or 3.13 fits this guide. Reopen the terminal. Check:

~~~powershell
python --version
~~~

If Windows opens the Store, try `py --version` and use `py` in place of `python` until you create the week-8 virtual environment. If neither works, revisit the installer's PATH option or Python's Windows instructions; do not change unrelated system settings.

Run a saved script with `python filename.py`. The standard-library labs need no package downloads.

## Week 5: Burp for hosted training labs

Get [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload). Use a temporary project and the built-in browser from Proxy → Open browser. Sign in to the Academy in your normal browser and launch the named lab; copy only the launched lab URL into Burp's browser.

Start with intercept OFF so pages load. Inspect HTTP history; send a relevant lab request to Repeater for one controlled change. Only use your assigned Academy lab instance. Do not route your normal banking or email browsing through the lab browser. Close the temporary project when finished.

## Week 8: isolated Django environment

[Lab 07](../labs/LAB-07-protected-notes.md) gives exact commands. It installs Django in `.venv` inside your exercise folder. Commands use that environment's Python directly, so changing PowerShell execution policy is unnecessary.

Local HTTP on `127.0.0.1` is for practice. Bind servers to loopback, keep them off public hosting, and stop them after studying. [Python's HTTP server](https://docs.python.org/3/library/http.server.html) is a development tool.

## Common fixes

| Symptom | Try this |
|---|---|
| File opens as text instead of a page | Check it is index.html, not index.html.txt |
| Browser says connection refused | Start the local server and keep its terminal open |
| Port 8000 is already in use | Stop your earlier server, or use 8001 in both command and URL |
| Template does not exist | Check the exact folders and filenames in Lab 07 |
| Login fails after setup | Confirm migrations ran and the fake user was created |
| Django reports missing module | Use the `.venv\Scripts\python.exe` command from the exercise |
| A lab is too hard | Repeat the normal request and explain it before changing it |

