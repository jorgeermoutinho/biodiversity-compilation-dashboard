# Biodiversity Literature Dashboard

An interactive, single-file web dashboard for visualising species occurrence records compiled from the scientific literature. Designed for researchers building biodiversity datasets from published sources.

No server, no installation, no dependencies to install — everything runs in the browser.

---

## Live demo

Hosted at: `https://your-site.netlify.app` *(replace with your URL after deployment)*

---

## What it does

- **Interactive map** — plots georeferenced records with colour-coded markers by phylum, family, publication, or type. Toggles between marker and heatmap view.
- **Taxonomic drilldown** — doughnut chart starting at phylum level; click any slice to drill down through class → order → family, with breadcrumb navigation.
- **Species / publication coverage** — horizontal bar chart showing how many unique species each publication contributes. Scrollable when dataset is large.
- **Species × publications frequency** — BOLD-style bar chart: x axis = number of publications a species has been recorded in, y axis = number of species with that count. Useful for assessing dataset completeness.
- **Cumulative new species** — tracks how many new species are added over time as publications are compiled.
- **Records and publications per year** — temporal overview of the literature compiled.
- **Monthly distribution** — shows seasonal bias in records.
- **Publication type breakdown** — pie chart of article, report, thesis, etc.
- **Global filters** — filter by phylum, class, order, family, publication, year, pub type, and free text. All charts and the map update simultaneously.
- **Stats strip** — live summary of total records, species, genera, publications, year range, georeferenced percentage, phyla, and families.

---

## How to use

### Option A — Google Sheets (recommended, auto-updates)

1. Keep your dataset in a Google Sheet with the columns described below.
2. In Google Sheets go to **File → Share → Publish to web**.
3. Select your data sheet/tab, change format to **CSV**, click **Publish**.
4. Copy the URL provided (looks like `https://docs.google.com/spreadsheets/d/…/pub?output=csv`).
5. Open the dashboard, click **⚙ configure source** in the top right.
6. Paste the URL in the **Google Sheets URL** tab → **Load data**.

The dashboard fetches fresh data every time the page is loaded. No manual exports needed.

> ⚠ This only works when the dashboard is served over `https://` (e.g. Netlify, GitHub Pages). It will not work when opening the HTML file directly from your computer due to browser security restrictions (CORS). Use the Paste CSV method in that case.

### Option B — Paste CSV (works locally, no hosting needed)

1. In Google Sheets go to **File → Download → Comma Separated Values (.csv)**.
2. Open the downloaded file in any text editor (Notepad, TextEdit, VS Code).
3. Select all (`Ctrl+A`) → Copy (`Ctrl+C`).
4. In the dashboard click **⚙ configure source** → **Paste CSV** tab → paste → **Load data**.

### Option C — Load demo data

Click **⚙ configure source** → **Load demo** to load the built-in example dataset (22 records of marine invertebrates and fish from Portuguese coastal waters, fully fictional).

A demo CSV is also provided in this repository as `demo_dataset.csv`.

---

## Dataset requirements

### Required columns

The column names are **case-insensitive** and **spaces are treated as underscores**. The following are recognised:

| Column | Description |
|---|---|
| `name_accepted` | Currently accepted species name (e.g. from WoRMS) |
| `name_used` | Name as used in the original publication |
| `genus` | Genus |
| `family` | Family |
| `order` | Order |
| `class` | Class |
| `phylum` | Phylum |
| `latitude` | Decimal degrees (e.g. `38.720097`). Positive = N, negative = S. |
| `longitude` | Decimal degrees (e.g. `-9.144234`). Positive = E, negative = W. |
| `coordinates_original` | Coordinates as reported in the publication (any format, for reference) |
| `source` | Full citation of the publication |
| `source_label` | Short label/code for the publication (e.g. `PER21`) |
| `year` | Year of the record (integer) |
| `month` | Month of the record (integer 1–12, optional) |
| `day` | Day of the record (integer, optional) |
| `publication_id` | Unique identifier for the publication (e.g. `PUB01`) |
| `journal` | Journal or outlet name |
| `pub_type` | Type of publication (`article`, `report`, `thesis`, `book chapter`, etc.) |

### Notes on coordinates

- Coordinates must be in **decimal degrees** — e.g. `11.530097` and `92.723434`.
- The parser handles both `.` and `,` as decimal separators.
- Records without valid coordinates are counted in the stats strip but not plotted on the map.
- The column name `lalitude` (common typo) is also accepted as an alias for `latitude`.

### Optional columns

Any additional columns in your sheet are silently ignored. You can add notes, DOIs, URLs, or any other fields freely.

### Minimum viable dataset

Only `name_accepted` and `phylum` are strictly required for the charts to render. Coordinates are needed for the map. `publication_id` and `source_label` are needed for the coverage and frequency charts.

---

## Deploying your own copy

### Netlify (simplest)

1. Rename `index.html` — it must be called `index.html`.
2. Put it in a folder.
3. Go to [netlify.com](https://netlify.com), log in, go to **Sites/Projects**.
4. Drag the folder onto the deploy zone.
5. Done — you get a `https://` URL immediately.

To update the dashboard file later, go to your site in Netlify → **Deploys** → drag the new folder.

### GitHub Pages

1. Create a new repository on [github.com](https://github.com).
2. Upload `index.html` (and optionally `demo_dataset.csv` and `README.md`).
3. Go to **Settings → Pages → Source → Deploy from branch → main → / (root) → Save**.
4. Your dashboard will be live at `https://yourusername.github.io/your-repo-name/`.

---

## Privacy

- Your Google Sheet stays **private** in your Google Drive at all times.
- The published CSV URL exposes data only to requests that know the exact URL — it does not make your sheet discoverable or searchable.
- The URL you configure is stored in your **browser's localStorage** only — it is never written into the HTML file and never uploaded to GitHub or Netlify.
- The dashboard itself (the HTML file on GitHub/Netlify) contains only the demo data and the visualisation code — no real data, no credentials.

---

## Technical notes

- Single self-contained HTML file — no build step, no npm, no framework.
- External libraries loaded from CDN: [Leaflet](https://leafletjs.com/) (map), [Chart.js](https://www.chartjs.org/) (charts), [PapaParse](https://www.papaparse.com/) (CSV parsing), [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat) (heatmap).
- Map tiles from [CartoDB](https://carto.com/basemaps/) via OpenStreetMap data.
- Fonts from Google Fonts (DM Serif Display, DM Mono, DM Sans).
- No data is sent to any external server. All processing happens locally in the browser.

---

## Demo dataset

`demo_dataset.csv` contains 22 fictional records of marine invertebrates and fish species from Portuguese coastal waters, spread across 10 fictional publications (2013–2022). It is provided solely to demonstrate the dashboard's functionality. **None of the records, species occurrences, or publication citations are real.**

---

## Licence

MIT — free to use, adapt, and share with attribution.
