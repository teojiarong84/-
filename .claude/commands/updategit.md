---
description: Security-scan, push to GitHub, ensure GitHub Pages is set up, and update the repo description
---

Run the following workflow, in order, stopping if any step fails:

1. **Secret scan (pre-publish check)**
   - Run `git status` and `git diff` (staged + unstaged) to see what is about to be committed.
   - Search the working tree (especially changed files) for likely secrets/credentials: API keys, tokens, passwords, private keys, `.env` files, AWS/GCP/Azure credentials, etc. Use Grep for patterns like `api[_-]?key`, `secret`, `password`, `token`, `BEGIN PRIVATE KEY`, `formsubmit` tokens, etc.
   - Confirm `.gitignore` excludes any local-only/sensitive files (e.g. `.env`, `.claude/settings.local.json`, credentials).
   - If anything sensitive is found, **stop** and report it to the user instead of committing/pushing.

2. **Commit and push**
   - Stage relevant changes (avoid `git add -A`/`git add .`; add specific files).
   - Create a concise commit message describing the change.
   - Push to `origin main`.

3. **GitHub Pages via GitHub Actions**
   - Check that [.github/workflows/static.yml](.github/workflows/static.yml) (or equivalent Pages deploy workflow) exists and is correctly configured for deploying the static site via `actions/deploy-pages`.
   - If it doesn't exist, create it.
   - Ensure the GitHub Pages source is set to "GitHub Actions" via `gh api` (e.g. `gh api -X PUT repos/{owner}/{repo}/pages -f build_type=workflow`), creating the Pages site first with `gh api -X POST repos/{owner}/{repo}/pages -f build_type=workflow` if it doesn't exist yet.

4. **Update repo "About"**
   - Use `gh repo edit` to set the repository description (and homepage URL to the GitHub Pages URL, and relevant topics) to reflect the current project (an investment strategy consultation landing page).

5. **Final security scan**
   - Run a final check over the diff that was pushed (`git show` / `git diff` of the last commit) to confirm nothing sensitive was published.
   - Summarize what was pushed, the Pages URL, and the updated About info to the user.

Confirm with the user before any destructive or hard-to-reverse action (force push, history rewrite, etc.) — none should be needed for this normal workflow.
