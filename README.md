# Shipley + Keighley and Ilkley — Leafletting Map

A canvassing and leafletting tracker for Shipley and Keighley and Ilkley (both Westminster constituencies, in full — 12 Bradford wards). Volunteers can view road-level status, plan routes, and mark progress in real time via a Google Sheets backend.

This repo is a **thin deployment** — it has no local `core.js`/`styles.css` of its own; both load directly from the primary [leaflet-map](https://github.com/Daemeous/leaflet-map) repo (see that repo's README, "Shared assets", for what that means and why).

Live: **https://daemeous.github.io/shipley/**

---

## Other live deployments

| Constituency / area | Site |
|---|---|
| Stafford | https://daemeous.github.io/leaflet-map/ |
| Demo | https://daemeous.github.io/leaflet-map-demo/ |
| South Hams | https://daemeous.github.io/south-hams/ |
| Burton & Uttoxeter | https://daemeous.github.io/burton-uttoxeter/ |
| Stone, Great Wyrley & Penkridge | https://daemeous.github.io/stone/ |
| Barnsley, Penistone & Stocksbridge | https://daemeous.github.io/barnsley/ |
| St Helens | https://daemeous.github.io/sthelens/ |

Related project — **[Pothole Watch](https://github.com/Daemeous/stafford-potholes)**, same visual style, separate Sheet/Apps Script backend.

The pipeline that builds this deployment's road/residence data and its Google Sheet + Apps Script backend lives in **[leaflet-pipeline](https://github.com/Daemeous/leaflet-pipeline)**, not in this repo.

---

## How it works

Road data is sourced from OpenStreetMap, clipped to ward boundaries verified against the OS Boundary-Line dataset, and given an estimated residence count per road (OS Open UPRN point-in-buffer matching). Each road is assigned to a ward, given a status (`Not_Started`, `Planned`, `In_Progress`, `Complete`), and stored in a Google Sheet. The app reads that sheet as a published CSV and renders roads as coloured polylines on a Leaflet map.

Authorised users can sign in with Google and update road statuses directly from the map, which writes back to the sheet via a Google Apps Script web app.

---

## Repository contents

| File | Purpose |
|------|---------|
| `index.html` | This deployment's config block (Sheet ID, Apps Script URL, title/subtitle, map centre) — the only thing that differs from any other deployment |
| `sw.js` | Service worker (must stay same-origin, so every deployment keeps its own copy even though `core.js`/`styles.css` are shared) |

`core.js`/`styles.css` are **not** in this repo — see [leaflet-map](https://github.com/Daemeous/leaflet-map)'s README before assuming a bug lives here; most app behaviour comes from that shared file.


---

## License

This project's own code (this frontend, and — in [leaflet-pipeline](https://github.com/Daemeous/leaflet-pipeline) — the data pipeline and Apps Script backends) is licensed under the **[PolyForm Noncommercial License 1.0.0](LICENSE)**: free to use, share, and modify for any non-commercial purpose, with attribution. Most of this repo (`core.js`/`styles.css`) is loaded from [leaflet-map](https://github.com/Daemeous/leaflet-map), which carries the same license. See [`LICENSE`](LICENSE) for the full text.

Copyright © Daniel Hodgkins.

That covers this project's own code only. The geographic data it displays comes from sources under their own separate licenses that explicitly permit commercial use (see Attributions below) — this project's non-commercial restriction doesn't, and legally can't, extend to that underlying data.

## Attributions

| Dependency | License | Notes |
|---|---|---|
| [Leaflet.js](https://leafletjs.com) | BSD-2-Clause | © Vladimir Agafonkin and contributors |
| [OpenStreetMap](https://www.openstreetmap.org/copyright) | [ODbL](https://opendatacommons.org/licenses/odbl/) | Map tiles and road data © OpenStreetMap contributors. Permits commercial use; requires attribution and share-alike for derivative databases. |
| OS Boundary-Line & OS Open UPRN | [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/) | © Crown copyright and database right, Ordnance Survey. Permits commercial use; requires attribution. |
| [Papa Parse](https://www.papaparse.com) | MIT | CSV parsing |
| [Turf.js](https://turfjs.org) | MIT | Geospatial analysis |
| Google Identity Services | [Google Terms of Service](https://policies.google.com/terms) | Sign-in, loaded from Google's own servers at runtime |
| [Overpass API](https://overpass-api.de) | [Usage policy](https://dev.overpass-api.de/overpass-doc/en/preface/commons.html) | OSM data queries (used by leaflet-pipeline) |
