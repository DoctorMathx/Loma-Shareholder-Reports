# Loma Microfinance Bank — Shareholder Reports

Official, self-contained interactive shareholder reports for Loma
Microfinance Bank.

The report is a single HTML file with all assets (fonts, images, audio,
CSS, JS) bundled inline — open it in any modern browser and the entire
report renders locally, with no network required.

## View the report

**Option 1 — open locally**

Download or clone the repo and double-click `index.html`. Modern Chrome,
Edge, Firefox, and Safari all work. No build step, no install.

**Option 2 — host on GitHub Pages**

This repo ships with a workflow (`.github/workflows/pages.yml`) that
publishes `index.html` to GitHub Pages on every push to `main`.

To turn it on:

1. Go to **Settings → Pages** in this repository.
2. Under **Build and deployment → Source**, choose **GitHub Actions**.
3. Push to `main` (or re-run the latest workflow). The site deploys to
   `https://<owner>.github.io/Loma-Shareholder-Reports/` and visitors
   land straight in the report.

## Soundtrack

The report includes a soundtrack ("Loma Dey For You") that autoplays as
soon as the browser allows. Modern browsers block unmuted autoplay
until the user has interacted with the page, so when autoplay is
rejected the player latches onto the very first click, tap, scroll, or
keypress and starts playing then. Visitors can also toggle playback
with the **Tap to play soundtrack** button in the corner.

## How the report renders

The HTML is produced by an inline "bundler" — a small script embedded
in `<head>` that, on `DOMContentLoaded`:

1. Reads the base64 asset manifest (`<script type="__bundler/manifest">`).
2. Optionally decompresses each asset with `DecompressionStream('gzip')`.
3. Creates `Blob` URLs for every asset.
4. Substitutes the asset UUIDs in the template with the live blob URLs.
5. Strips `integrity` / `crossorigin` attributes (blob URLs inherit a
   `null` origin under `file://`, which would otherwise be rejected by
   Subresource Integrity).
6. Replaces `<html>` with the unpacked document and re-creates each
   `<script>` so it executes (DOM-inserted scripts are inert per spec).
7. Attempts to autoplay the soundtrack; on rejection, arms a
   one-shot listener for the first user gesture.

Because everything is decoded client-side, the file is fully portable —
email it, drop it on a USB stick, or host it anywhere static files are
served.

## Repository layout

```
.
├── .github/workflows/pages.yml   # Auto-deploy to GitHub Pages
├── .nojekyll                     # Disable Jekyll processing
├── index.html                    # The report (self-contained, ~24 MB)
└── README.md
```

---

© Loma Microfinance Bank Limited
