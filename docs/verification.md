# Verification Record

Every check listed below was actually run. Nothing here is assumed.

## Current source-to-page mapping

| Source file (current name) | Flyer | Website page | Transcription |
|---|---|---|---|
| `Image/nitzan-ashdod-page-01.jpg` | Nitzan services: lessons, diagnoses, treatments | `public/index.html` | `docs/content/page-01-transcription.txt` |
| `Image/nitzan-ashdod-page-02.jpg` | B•Friendly social skills group | `public/page2.html` | `docs/content/page-02-transcription.txt` |

The source files were renamed by the owner on 2026-10-28 to set this order. The site was updated to match; the source files themselves were not renamed again.

## Round 2 – 2026-10-28 (page-order change and English documentation)

### Local checks

| Check | Method | Result |
|---|---|---|
| Source file identity | Visual inspection of both current images | `page-01` = services flyer, `page-02` = B•Friendly flyer |
| Content mapping | Script: every line of each transcription must appear in its mapped page | `index.html` ← page-01: 11/11 lines present. `page2.html` ← page-02: 21/21 lines present |
| Wrong-page content | Same script: lines from one transcription found on the other page | None |
| Inline CSS/JS | Search for `style=`, `<style>`, `<script>`, inline event handlers | None found; no JavaScript files exist |
| Base-path safety | Search for `src="/` and `href="/` | None found; all paths are relative (`./`) |
| Footer credit | Exact string `Built and developed by Oren Salami` | Present once on each page |
| HTTP under `/nitzan-ashdod/` | Local `python -m http.server`, site copied into a `nitzan-ashdod/` subfolder; `curl` | `index.html`, `page2.html`, `assets/css/styles.css`: all 200 |
| Layout | Headless Chromium (Playwright), both pages at 375, 768 and 1440 px, full-page screenshots reviewed | No horizontal overflow at any width; layout renders as intended |
| Navigation | Click index → page2 → index via the header nav | Worked in both directions; `aria-current` on the correct item |
| Keyboard | Tab from page load | Focus goes to the skip link, then the brand link, with a visible focus ring |
| Console / network | Browser report | 0 console errors or warnings, 0 failed requests |

### Live-site checks

At the time of Round 2, GitHub Pages was not enabled (`GET /repos/Oren1984/nitzan-ashdod/pages` returned 404), so no live checks were possible. See Round 3.

## Round 3 – 2026-10-28 (first live deployment)

### Deployment

| Step | Result |
|---|---|
| Pages enabled by the owner: `gh api -X POST repos/Oren1984/nitzan-ashdod/pages -f build_type=workflow` | `build_type: workflow`, `html_url: https://oren1984.github.io/nitzan-ashdod/` |
| Workflow run `40704928364` (`workflow_dispatch`, commit `8d5b702`) | `success` – Checkout, Configure Pages, Upload artifact and Deploy all succeeded |

### Live-site checks

| Check | Method | Result |
|---|---|---|
| HTTP status | `curl` | `/nitzan-ashdod/` 200 `text/html`; `/nitzan-ashdod/page2.html` 200 `text/html`; `/nitzan-ashdod/assets/css/styles.css` 200 `text/css` |
| Deployed content | Live HTML compared byte-for-byte with `public/index.html` and `public/page2.html` at commit `8d5b702` | Identical |
| Page titles | Live `<title>` | index: "שיעורים, אבחונים וטיפולים \| ניצן אשדוד"; page2: "קבוצת B•Friendly לטיפוח כישורים חברתיים \| ניצן אשדוד" |
| Footer credit | Exact string on live pages | Present once on each page |
| Layout | Headless Chromium, both live pages at 375, 768 and 1440 px, screenshots reviewed | Stylesheet applied; no horizontal overflow at any width |
| Navigation | index → page2 → index on the live site | Worked in both directions |
| Console / network | Browser report | 0 console errors or warnings, 0 failed requests |

Local checks were not repeated in Round 3, because no site files changed after Round 2.

## Round 1 – 2026-10-28 (initial build, previous page order)

Performed on the first version, in which the B•Friendly flyer was the home page. Superseded by Round 2 where the two overlap.

- Visual transcription of both flyers, including zoomed crops of small text regions.
- Script check that all transcription lines appeared in the HTML: passed.
- Static checks for inline CSS/JS and root-absolute paths: none found.
- Headless Chromium at 375, 768 and 1440 px: no overflow, navigation worked, 0 console errors. Two layout fixes were made as a result (an empty grid cell on desktop for the notes page, and a dangling "|" separator in the mobile contact line).
- First deployment run (`40701800624`) failed at "Configure Pages" because Pages was not enabled. No live checks were possible.

## Known limitations

- The logos (Nitzan, B•Friendly) exist only inside photographs of the printed flyers, at a quality unsuitable for the web, so the brand is rendered as text. An original logo file can be added under `public/assets/images/`.
- The children's photo on the B•Friendly flyer and the illustration at the bottom of the services flyer were not reproduced (decorative imagery, not content).
- The Facebook icon on the B•Friendly flyer has no page address, so no Facebook link was added.
- The handwritten-style font of the services flyer was not reproduced; system fonts with Hebrew support are used.
- Not tested with a screen reader, or in Safari or Firefox.
- "Works without JavaScript" holds by construction (the site has no JavaScript); it was not tested separately with JavaScript disabled.
