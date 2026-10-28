# ניצן אשדוד – אתר

אתר סטטי קטן לעמותת **ניצן אשדוד**, שעוזרת לילדים ובוגרים עם ליקויי למידה. האתר נבנה במתנה לעמותה. התוכן הועתק מילה במילה משני פלאיירים של העמותה.

## העמודים

| עמוד | קובץ |
|---|---|
| קבוצת B•Friendly לטיפוח כישורים חברתיים | `public/index.html` |
| שיעורים, אבחונים וטיפולים | `public/page2.html` |

## מבנה

```
public/                 האתר שמתפרסם (HTML, CSS)
  assets/css/styles.css עיצוב משותף
docs/content/           תמלול התוכן מהפלאיירים
docs/*.md               תחזוקה, פריסה, תיעוד בדיקות
.github/workflows/      פריסה ל-GitHub Pages
```

## תצוגה מקומית (Windows / VS Code)

```powershell
cd public
python -m http.server 8000
```

ואז לפתוח http://localhost:8000/ . אפשר גם לפתוח את `public/index.html` ישירות בדפדפן.

## עריכה

- טקסט: לערוך ישירות ב-`public/index.html` או ב-`public/page2.html`.
- עיצוב: `public/assets/css/styles.css`.
- פרטים נוספים: [`docs/maintenance.md`](docs/maintenance.md).

## פריסה

כל `push` לענף `main` מפרסם את `public/` ל-GitHub Pages דרך GitHub Actions. פרטים: [`docs/deployment.md`](docs/deployment.md).

כתובת האתר: https://oren1984.github.io/nitzan-ashdod/

---

Built and developed by Oren Salami
