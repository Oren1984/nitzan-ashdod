# Site Maintenance

## Where to edit each page

| Page | File | Content source |
|---|---|---|
| 1 – Lessons, diagnoses and treatments (home page) | `public/index.html` | `docs/content/page-01-transcription.txt` |
| 2 – B•Friendly social skills group | `public/page2.html` | `docs/content/page-02-transcription.txt` |

Edit the text directly in the HTML. There is no build step: whatever is in `public/` is what gets published.

## Shared styling

- All styling lives in a single file: `public/assets/css/styles.css`.
- Colors are defined as custom properties at the top of the file (`:root`), for example `--green-dark` and `--note-pink`.
- Each page selects its visual theme with a class on `<body>`:
  - `public/index.html`: `class="theme-notes"` (pastel note cards)
  - `public/page2.html`: `class="theme-bfriendly"` (green B•Friendly theme)
- Do not add CSS inside the HTML (`style=` attributes or `<style>` blocks).
- The site has no JavaScript. If some is ever needed, add an external file under `public/assets/js/` and load it with `defer`.

## Adding or replacing images

1. Put the file in `public/assets/images/`. Use lowercase English filenames, because GitHub Pages is case-sensitive.
2. Reference it with a relative path: `<img src="./assets/images/logo.png" alt="Hebrew description" width="..." height="...">`.
3. Never use a path that starts with `/`. It breaks under the `/nitzan-ashdod/` project path.
4. The original flyer images (`Image/`) are source material only and are not tracked in Git.

## RTL and mobile layout

- Keep `<html lang="he" dir="rtl">` on both pages.
- English text, phone numbers and email addresses are wrapped with `dir="ltr"` (and `lang="en"` for English) so they display correctly.
- Prefer logical CSS properties (`margin-inline`, `padding-inline-start`, `inset-inline-start`) over left/right.
- Breakpoints: `700px` (tablet) and `1024px` (desktop). The base styles target mobile.
- After a change, check at 375, 768 and 1440 px wide that there is no horizontal scrolling.

## Updating the footer

The footer is at the end of each HTML file (`<footer class="site-footer">`). Update both files. The credit line must remain exactly:

```
Built and developed by Oren Salami
```

## Comparing content with the source

1. Open the transcription in `docs/content/` and the matching HTML page side by side.
2. Confirm every line in the transcription appears on the page with the same wording and spelling.
3. Notes about uncertain or non-transcribed elements are at the end of each transcription file, under "הערות / אי-ודאות".
4. If the source content changes, update the transcription first, then the HTML.
