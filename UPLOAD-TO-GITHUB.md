# Replace the ZIP with the actual repository files

**Repository:** [swtnness/web-security-to-banking-security](https://github.com/swtnness/web-security-to-banking-security)  
**Checked:** 2026-10-11. The connected GitHub account had read access but no push permission. No remote changes were made.

The inspected main branch contained README.md and **web-security-to-banking-security.zip**. The archive held the original outline. This package expands that outline and keeps its original navigation paths working.

## Recommended: upload with your browser

1. Open this package's **web-security-to-banking-security** folder in File Explorer. You should see README.md, curriculum, labs, progress and the numbered folders immediately inside it.
2. If you downloaded the optional delivery ZIP, right-click it → **Extract All** first. Open the extracted inner folder until README.md is visible. **Do not upload either ZIP.**
3. Sign in to GitHub as **swtnness**, or an account with write permission. Open the repository link above and choose the **main** branch.
4. Select **Add file → Upload files**. From Explorer, drag the **contents of the prepared folder** into the upload area, including all subfolders and .gitignore. Do not drag its outer web-security-to-banking-security folder.
5. Inspect the paths before committing. Correct: `README.md`, `curriculum/WEEK-01.md`, `labs/LAB-01-http.md`. Incorrect: `web-security-to-banking-security/README.md` nested under the repository root.
6. Commit with the message **Add complete 16-week security curriculum and labs**. Replacing the existing README is intentional. If GitHub requires a branch, name it `add-security-curriculum`, then open a pull request into main and review/merge it.
7. On main, open README and click **Start today**, **Week 1**, **Security labs** and **Progress tracker**. Check the files render as Markdown.
8. Only after those files are present, open the old **web-security-to-banking-security.zip** in the GitHub repository. Use its file menu → **Delete file**. Commit **Remove archive after adding extracted learning files**. If you used a protected branch, follow its pull-request flow.
9. Check that main has the folders and no old ZIP. Keep a private/local backup if desired; ordinary Git history still preserves the earlier commit.

GitHub documents [browser uploads](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository) and [file deletion](https://docs.github.com/en/repositories/working-with-files/managing-files/deleting-files-in-a-repository). If the browser does not accept folders, use the Git route below or GitHub Desktop's local repository folder.

## Expected top level

~~~text
.gitignore
README.md
RESOURCES.md
SECURITY.md
UPLOAD-TO-GITHUB.md
00-start-here/
01-web-foundations/
02-web-vulnerabilities/
03-defensive-engineering/
04-banking-security/
05-portfolio-projects/
curriculum/
labs/
progress/
templates/
~~~

There should be 16 WEEK files under curriculum and 12 LAB files under labs. The progress boxes should all still be empty.

## Alternative: existing or new Git clone

Use a clean clone of the named repository. Copy the prepared folder's **contents** into the clone, replacing README.md. Do not copy .git from any other folder. Do not overwrite unrelated local work; inspect git status first.

In PowerShell **inside that clone**, run these commands in order:

~~~powershell
git status
git switch -c add-security-curriculum
git add README.md RESOURCES.md SECURITY.md UPLOAD-TO-GITHUB.md .gitignore
git add 00-start-here 01-web-foundations 02-web-vulnerabilities 03-defensive-engineering
git add 04-banking-security 05-portfolio-projects curriculum labs progress templates
git rm -- web-security-to-banking-security.zip
git diff --cached --stat
git diff --cached
git commit -m "Replace ZIP with complete security learning repository"
git push -u origin add-security-curriculum
~~~

Review the staged files before the commit command. If the old ZIP is already absent, skip git rm. If the branch already exists, switch to it instead of creating it again. Resolve any unexpected changes before continuing; never force-push as a fix.

Open the repository's proposed pull request, choose base main and review the file changes. Merge when the paths and content are correct. You should see the expanded README on main after merging.

## Repository appearance

In the repository's About settings, use:

**Description:** Beginner-first, 16-week path from web fundamentals to defensive web development and simulated banking security, with labs and a progress tracker.

**Topics:** cybersecurity, web-security, application-security, learning-roadmap, owasp, secure-coding, payment-security, portfolio.

No GitHub Pages deployment is needed: Markdown renders directly in the repository.

## If something looks wrong

- **No upload/edit controls:** confirm the signed-in account has write access.
- **README links return 404:** check main contains the folders directly at its root, preserving capitalization.
- **Only a ZIP appears:** extract locally and upload its contents.
- **.gitignore was missed:** create a new file named exactly .gitignore and paste the supplied file's contents.
- **New unrelated work appeared remotely:** review it before replacing overlapping files; this package reflects the inspection date above.

