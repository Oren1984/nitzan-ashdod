# פריסה (GitHub Pages)

## תצורה

- מאגר: `Oren1984/nitzan-ashdod`, ענף `main`.
- Settings > Pages > Build and deployment > Source: **GitHub Actions**.
- Workflow: `.github/workflows/deploy-pages.yml`.
  - רץ על כל `push` ל-`main`, וגם ידנית (`workflow_dispatch`).
  - מעלה **רק** את התיקייה `public/` (`actions/upload-pages-artifact`, `path: public`).
  - פורס עם `actions/deploy-pages` לסביבה `github-pages`.
  - הרשאות מינימליות: `contents: read`, `pages: write`, `id-token: write`.
  - `concurrency: pages` — פריסה אחת בכל פעם, בלי לבטל פריסה שכבר רצה.
- `public/.nojekyll` — מונע עיבוד Jekyll.
- כתובת: https://oren1984.github.io/nitzan-ashdod/

## הרשאות נדרשות

- הרשאת כתיבה (push) למאגר כדי לפרסם עדכונים.
- הרשאת Admin רק להגדרת Pages בפעם הראשונה (Source = GitHub Actions).

## פרסום עדכון

```powershell
git add public docs
git commit -m "Update page content"
git push
```

הפריסה מתחילה אוטומטית. מעקב:

```powershell
gh run list --workflow deploy-pages.yml --limit 3
gh run watch
```

## בדיקת כשל בפריסה

1. GitHub > Actions > "Deploy to GitHub Pages" > הריצה שנכשלה > לפתוח את השלב האדום.
2. משורת הפקודה: `gh run view --log-failed`.
3. בעיות נפוצות:
   - Pages לא מוגדר ל-GitHub Actions → Settings > Pages > Source: GitHub Actions.
   - חוקי הגנה של הסביבה `github-pages` לא מאפשרים את הענף → Settings > Environments > github-pages.
4. הרצה חוזרת: `gh run rerun <run-id>` או `gh workflow run deploy-pages.yml`.

## ביטול שינוי שגוי

לא לשכתב היסטוריה ולא להשתמש ב-force push. ליצור commit הפוך:

```powershell
git log --oneline -5
git revert <commit-sha>
git push
```

ה-push מפעיל פריסה חדשה עם המצב הקודם.
