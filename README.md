# Loma Microfinance Bank — Shareholder Reports

Official, self-contained interactive shareholder reports for Loma Microfinance Bank.

Each report is a single HTML file with all assets (fonts, images, audio, CSS, JS)
bundled inline — open it in any modern browser and the entire report renders
locally, with no network required.

## Contents

| Report | File |
|---|---|
| Mid-Year Shareholders Report — June 2026 | [`Loma Mid-Year Shareholders Report (standalone).html`](Loma%20Mid-Year%20Shareholders%20Report%20%28standalone%29.html) |

A small landing page ([`index.html`](index.html)) lists all reports with cover
art and quick links.

## View the reports

**Option 1 — open locally**

Download or clone the repo and double-click `index.html` (or any
`*.html` report file). Modern Chrome, Edge, Firefox, and Safari all
work. No build step, no install.

**Option 2 — host on GitHub Pages**

This repo ships with a workflow (`.github/workflows/pages.yml`) that
publishes the landing page and all reports to GitHub Pages on every
push to `main`.

To turn it on:

1. Go to **Settings → Pages** in this repository.
2. Under **Build and deployment → Source**, choose **GitHub Actions**.
3. Push to `main` (or re-run the latest workflow). The site will deploy
   to `https://<owner>.github.io/Loma-Shareholder-Reports/`.

## How the report renders

The standalone HTML is produced by an inline "bundler" — a small script
embedded in `<head>` that, on `DOMContentLoaded`:

1. Reads the base64 asset manifest (`<script type="__bundler/manifest">`).
2. Optionally decompresses each asset with `DecompressionStream('gzip')`.
3. Creates `Blob` URLs for every asset.
4. Substitutes the asset UUIDs in the template with the live blob URLs.
5. Strips `integrity` / `crossorigin` attributes (blob URLs inherit a
   `null` origin under `file://`, which would otherwise be rejected by
   Subresource Integrity).
6. Replaces `<html>` with the unpacked document and re-creates each
   `<script>` so it executes (DOM-inserted scripts are inert per spec).

Because everything is decoded client-side, the file is fully portable —
email it, drop it on a USB stick, or host it anywhere static files are
served.

## Repository layout

```
.
├── .github/workflows/pages.yml       # Auto-deploy to GitHub Pages
├── .nojekyll                         # Disable Jekyll processing
├── index.html                        # Landing page (lists all reports)
├── Loma Mid-Year Shareholders Report (standalone).html
└── README.md
```

## Adding a new report

1. Drop the new standalone `.html` file at the repository root.
2. Add an entry to the `Contents` table above.
3. Add a new `<article class="card">` block to `index.html` (copy an
   existing one and adjust title, date, description, and `href`).
4. Commit and push — the Pages workflow takes care of the rest.

---

© Loma Microfinance Bank Limited
