# Week 2 — Terminal and Git without overwhelm

**Prerequisites:** Week 1: identify a request and response.

**Time:** six 60-minute sessions; Day 7 is rest or catch-up. For each session, read for about 15 minutes, practice for 35 and write evidence for 10. Split a difficult session over two days if necessary.

## Understand

A terminal runs commands in a current folder. Git tracks changes in a repository; a commit is a local snapshot, while a push sends commits to GitHub. You can practice both without a Linux installation.

## Do these sessions in order

1. **Day 1.** Read the Git section in [Setup](../00-start-here/SETUP.md). In PowerShell, run `Get-Location` and `Get-ChildItem`. Write what a path, folder and file mean.

2. **Day 2.** In a separate scratch folder, use `New-Item -ItemType Directory git-practice`, `Set-Location git-practice`, and `Set-Content notes.txt 'My first security note'`. Read it with `Get-Content notes.txt`. Confirm the file in Explorer.

3. **Day 3.** Run `git init` in that scratch folder only, then `git status`, `git add notes.txt`, and `git commit -m "Add first note"`. If identity is missing, follow Setup. Run `git log --oneline` and explain each command.

4. **Day 4.** Change one line in notes.txt. Run `git diff`, stage the file and run `git diff --cached`. Explain the difference between unstaged, staged and committed changes. Commit this revision.

5. **Day 5.** Compare PowerShell commands with common Linux equivalents: `Get-Location`/`pwd`, `Get-ChildItem`/`ls`, `Set-Location`/`cd`, `Get-Content`/`cat`. Read about processes; locate your browser in Task Manager without ending it.

6. **Day 6.** Apply the workflow to one sanitized note in your real repository. Use the browser editor if Git authentication blocks you. Explain why .gitignore does not remove an already tracked secret.

## Evidence

Save `progress/week-02.md` with a command cheat sheet, two local commit identifiers, and the difference between local Git and GitHub.

## Checkpoint

From a new terminal, can you find the scratch folder, explain a diff and save one reviewed change? If not, repeat sessions 2–4.

Reading: [Git's beginner book](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control).

[Previous](WEEK-01.md) · [Next](WEEK-03.md) · [Roadmap](ROADMAP.md) · [Progress](../progress/PROGRESS.md)

