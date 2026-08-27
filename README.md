<p align="center">
  <img src="logo.svg" width="96" height="96" alt="Topsheet & Receipt Organiser logo">
</p>

# Topsheet & Receipt Organiser

_Created by Hyman._

A single-page tool for assembling a credit-card payment pack: it reads your
statement and your AutoEntry export, matches each receipt PDF to the right
topsheet, sorts everything into statement order, and exports one print-ready
merged PDF plus a Sage import CSV.

Everything runs **in your own browser**. No statement, receipt, or export data is
ever uploaded — the PDFs are read and merged locally on your machine.

## Live site

Once published with GitHub Pages (see below), the tool loads at:

```
https://<your-username>.github.io/<repo-name>/
```

## How to use

### Step 1 — Build sequence
1. Paste your **credit-card statement** (headers and all) into the left box. The
   tool keeps only real transaction lines, uses the transaction date, skips
   fees/headers/footers, and excludes refunds. This is the master order.
2. Paste your **AutoEntry export** (with its header row) into the right box.
   Columns used:
   - `SupplierDescription` — payee
   - `BaseCurrencyTotal` — amount
   - `Description` — description
   - `AccountCode` — nominal code (for Sage)
   - `AccountCodeDescription` — department
   - `Reference` — payment requested by
   - `InvoiceDate` — date
3. Click **Order export to statement**. Amounts are auto-corrected against
   AutoEntry, and you get one ordered sequence table. Orange rows are statement
   lines with no clean AutoEntry match.

### Step 2 — Load PDFs
1. Drop your **topsheets PDF** (one topsheet per page).
2. Drop **all your individual receipt PDFs at once**. One file = one receipt, so
   multi-page receipts are kept together automatically.

### Step 3 — Match & order
- **Auto-match by text** reads each receipt's payee and total and pairs it to the
  right topsheet.
  - **Green** = confident (receipt total matches and the payee agrees).
  - **Amber** = matched but worth a glance.
  - Uncertain ones are left **unmatched** rather than guessed.
- Click a matched card to **verify** the topsheet and receipt side by side, then
  **✓ Confirm** to lock it in. Confirmed and manual matches survive re-running
  auto-match and re-dropping receipts.
- Fix any match by dragging a receipt onto a topsheet, or use **Match →** on a
  receipt then click the target topsheet.
- **↕ Sort to statement order** arranges the pack to follow the statement, using
  the payee name (plus amount and date) to line each topsheet up with its
  statement line. Reorder any card by dragging its header, or with the ▲▼ / number.
- **Clear all** resets the matches (asks first).

### Step 4 — Export
- **Merged PDF** — each topsheet followed by its matched receipt page(s), in
  order. Original pages are copied losslessly.
- **Sage import CSV** — two options:
  - **All transactions** — every line on the statement.
  - **Recognised only** — every line the sequence builder matched to your
    AutoEntry export (i.e. all rows except the red/unmatched ones).

### Starting a new month
Use **↺ Start over (new month)** on Step 1 to clear the statement, the loaded
PDFs, and all matches for a fresh run.

## Publishing to GitHub Pages

1. Create a new **public** repository on GitHub.
2. **Add file → Upload files** and upload `index.html` (and this `README.md`).
3. **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch **main**, folder **/ (root)**, then **Save**.
4. Wait ~1 minute; the site goes live at the URL shown on that Pages screen.

To update later, upload a new `index.html` over the old one and commit — the site
refreshes automatically.

## Privacy

The repository (code) is public, but it contains only the tool. It stores nothing
and uploads nothing. **Do not commit real statements or receipt PDFs** to the
repo — the app doesn't need them stored anywhere.

## Notes

- Works in any modern browser (built and tested on Chrome/Safari).
- PDF reading and page rendering use pdf.js; the lossless merge uses pdf-lib.
  Both load from a CDN, so the live site needs an internet connection the first
  time it opens.

## License

Copyright © 2026 Hyman. You're free to use, copy, modify, and share this tool —
including inside a business — but you may **not sell it or charge for it** (or any
modified version) without the author's written permission. Keep the credit line
intact. See [`LICENSE`](LICENSE) for the full terms.
