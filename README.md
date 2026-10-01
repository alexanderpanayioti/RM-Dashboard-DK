# OODK Dashboard

Ocean Outdoor Denmark — out-of-home (OOH) ad spend dashboard, built from Fifty5Blue Adfacts exports.

**Live:** https://alexanderpanayioti.github.io/RM-Dashboard-DK/
**Password:** `OODK2026`

## What it shows

- **Overview** — KPIs, spend by media vehicle (yearly + monthly trend + stacked monthly), vehicle market share, top 10 product groups, top clients, yearly/monthly detail tables, annual growth
- **Target Clients** — prospecting view: advertisers with no Ocean Outdoor spend, below/above-average Ocean Outdoor share, and year-over-year decliners (both total spend and Ocean Outdoor-specific)
- **All Advertisers** — full searchable list across all 1,735 advertisers
- **Support** — request form that opens a pre-filled email draft

An Excel export (filtered to the current selection, or the full dataset) is available from the two buttons in the header.

## Data

- **Source:** Fifty5Blue Adfacts Explorer export, covering Ocean Outdoor, AFA, and Bauer Media Outdoor
- `Data.csv` is the **raw, unmodified export file** straight out of Adfacts Explorer — the standard "Report from Adfacts Explorer" format, Danish number formatting and all
- `index.html` fetches `Data.csv` at runtime and does all the parsing in the browser (skips the report's header lines, converts the Danish `1234,56` spend format, reads year/month out of the `2023, 03) Marts` field) — no conversion step, no script
- As of the last update: Jan 2023 – Sep 2026 (45 months), 18,783 rows, 133 product groups

## Updating with a new export

1. Export a fresh CSV from Adfacts Explorer.
2. Rename it to `Data.csv` and replace the one in this repo. That's it — no script to run.
3. Commit and push:
   ```bash
   git add Data.csv
   git commit -m "Update data through <month> <year>"
   git push
   ```

The live page picks up the change automatically within a minute or two. `index.html` never needs to change for a data update.

### Previewing locally before you push

Because `index.html` *fetches* `Data.csv`, opening the file directly in a browser (`file://...`) won't load the data — browsers block that kind of fetch for local files. To preview a change before pushing, run a tiny local server from this folder and open the page through it instead:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/ in your browser
```

## Tech stack

- Vanilla JS + [Chart.js](https://www.chartjs.org/) 4.4.1 for charts
- [PapaParse](https://www.papaparse.com/) 5.4.1 for parsing `Data.csv`
- [SheetJS](https://sheetjs.com/) (`xlsx.full.min.js`) for the Excel export
- DM Sans / DM Mono (Google Fonts)
- [GoatCounter](https://www.goatcounter.com/) analytics — site `rmutomhusdk`
- No build step, no npm install, nothing to run — just two files

## Files

| File | Purpose |
|---|---|
| `index.html` | The dashboard. Static — doesn't change when the data updates. |
| `Data.csv` | The raw Adfacts Explorer export. This is the only file that changes each update — just swap it. |
| `README.md` | This file |
