# NPA KPI Dashboard — MON Amata Factory

Static dashboard reading live data from a Google Sheet. No build step, no server — plain HTML/CSS/JS.

## How it works

Every page fetches the same published CSV from the Google Sheet ("NPA KPI" tab) and renders the numbers client-side. `index.html` shows all 16 KPI cards; each `npa_*.html` is the detail page for one KPI (trend chart, monthly table, definition).

## Hosting on GitHub Pages

1. Push all files in this folder to a GitHub repo (root, or a `/docs` folder).
2. Repo -> Settings -> Pages -> Source: pick the branch/folder above -> Save.
3. GitHub gives you a URL like `https://<user>.github.io/<repo>/` -- that's your dashboard.
4. No further config needed; every page pulls fresh data from the Google Sheet on load (and auto-refreshes hourly).

## Google Sheet requirements

The sheet must stay shared as "Anyone with the link can view" (File -> Share), otherwise the CSV export used by every page (`CSV_URL` in each `<script>` block) will fail to load.

## Updating KPI data

Add/edit values directly in the Google Sheet "NPA KPI" tab: one row per KPI, one column per month (`January`...`December`), plus `Target` and `Unit`. The dashboard picks up new values automatically -- nothing to redeploy.

## Adding a new KPI card

1. Add a row to the Google Sheet with the exact KPI name you'll use below.
2. Duplicate any `npa_*.html` file, rename it, and edit only the `var ROW=...` line plus the bilingual TH/EN title/definition/calculation/target strings (all clearly marked near the top of the `<script>` block).
3. Add one entry to the `KPI_CFG` array in both `index.html` and `npa_index.html` (row name, TH/EN labels, category `sp`/`q`/`o`, filename).

## Files

- `index.html`, `npa_index.html` -- dashboard home (identical content, kept for backward-compatible links)
- `npa_safety.html`, `npa_care_compliance.html`, `npa_open_vacancy.html`, `npa_turnover.html`, `npa_damage.html`, `npa_complaint.html`, `npa_dispatch.html`, `npa_ira.html`, `npa_truck.html` -- original 9 KPIs
- `npa_because_we_care.html`, `npa_safety_tag.html`, `npa_near_miss.html`, `npa_safer_easier.html`, `npa_legal_compliance.html`, `npa_grow_coaching.html`, `npa_manpower_fulfill.html` -- 7 new KPIs added August 2026

Rebuilt from scratch on 2026-08-25 -- single canonical template, no leftover text from earlier versions.
