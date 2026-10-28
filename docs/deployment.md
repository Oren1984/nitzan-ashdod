# Deployment (GitHub Pages)

## Configuration

- Repository: `Oren1984/nitzan-ashdod`, branch `main`.
- Settings > Pages > Build and deployment > Source: **GitHub Actions**.
- Workflow: `.github/workflows/deploy-pages.yml`.
  - Runs on every `push` to `main`, and manually (`workflow_dispatch`).
  - Uploads **only** the `public/` folder (`actions/upload-pages-artifact`, `path: public`).
  - Deploys with `actions/deploy-pages` to the `github-pages` environment.
  - Minimal permissions: `contents: read`, `pages: write`, `id-token: write`.
  - `concurrency: pages` – one deployment at a time, without cancelling one already in progress.
- `public/.nojekyll` – disables Jekyll processing.
- Expected URL: https://oren1984.github.io/nitzan-ashdod/

## Current status

GitHub Pages is **not yet enabled** for the repository, so the workflow fails at the "Configure Pages" step. One-time fix (requires admin access), either:

- Settings > Pages > Build and deployment > Source: **GitHub Actions**, or
- `gh api -X POST repos/Oren1984/nitzan-ashdod/pages -f build_type=workflow`

Then re-run the latest workflow: `gh workflow run deploy-pages.yml`.

## Required permissions

- Write (push) access to the repository to publish updates.
- Admin access only for the one-time Pages setup (Source = GitHub Actions).

## Publishing an update

```powershell
git add public docs
git commit -m "Update page content"
git push
```

Deployment starts automatically. To follow it:

```powershell
gh run list --workflow deploy-pages.yml --limit 3
gh run watch
```

## Investigating a failed deployment

1. GitHub > Actions > "Deploy to GitHub Pages" > the failed run > open the red step.
2. From the command line: `gh run view --log-failed`.
3. Common causes:
   - Pages is not set to GitHub Actions → Settings > Pages > Source: GitHub Actions.
   - Protection rules on the `github-pages` environment do not allow the branch → Settings > Environments > github-pages.
4. To retry: `gh run rerun <run-id>` or `gh workflow run deploy-pages.yml`.

## Reverting a bad change

Do not rewrite history or force-push. Create a reverting commit instead:

```powershell
git log --oneline -5
git revert <commit-sha>
git push
```

The push triggers a new deployment with the previous state.
