# Nitzan Ashdod – Website

A small static website for **Nitzan Ashdod** (ניצן אשדוד), an organization supporting children and adults with learning disabilities. The site was built as a gift for the organization. Its Hebrew content is transcribed verbatim from two of the organization's flyers.

## Pages

| Order | Page | File | Source |
|---|---|---|---|
| 1 | Lessons, diagnoses and treatments (שיעורים, אבחונים וטיפולים) | `public/index.html` | `Image/nitzan-ashdod-page-01.jpg` |
| 2 | B•Friendly social skills group (קבוצת B•Friendly) | `public/page2.html` | `Image/nitzan-ashdod-page-02.jpg` |

## Directory overview

```
public/                  Deployed website (HTML, CSS)
  assets/css/styles.css  Shared stylesheet
docs/content/            Verbatim Hebrew transcriptions of the flyers
docs/*.md                Maintenance, deployment and verification notes
.github/workflows/       GitHub Pages deployment
```

The source flyers in `Image/` are reference material only and are not committed.

## Local preview (Windows / VS Code)

In the VS Code terminal:

```powershell
cd public
python -m http.server 8000
```

Then open http://localhost:8000/ . Opening `public/index.html` directly in a browser also works.

## Maintenance

- Edit page text directly in `public/index.html` or `public/page2.html`.
- Edit styling in `public/assets/css/styles.css`.
- Details: [`docs/maintenance.md`](docs/maintenance.md).

## Deployment

Every push to `main` deploys `public/` to GitHub Pages through GitHub Actions. Details: [`docs/deployment.md`](docs/deployment.md).

**Status:** not live yet. GitHub Pages has not been enabled for the repository (Settings > Pages > Source: GitHub Actions). The expected URL is https://oren1984.github.io/nitzan-ashdod/ ; it will be marked as live here only after a deployment has been verified.

---

Built and developed by Oren Salami
