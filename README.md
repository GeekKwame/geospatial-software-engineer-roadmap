# Geospatial Software Engineer Roadmap

A 26-week, project-based path from **backend engineer with one GIS project** to **geospatial software engineer** who can own farm, forest and nursery mapping systems.

Built and followed in public by [Blessing Edmund Kwame Dogbe](https://github.com/GeekKwame) (Accra, Ghana), Software Engineer at Afarinick Company Limited. When the journey is finished, this repo is meant to be a **guide for other developers** who want the same path.

> **Not a tutorial dump.** Each phase has a week-by-week plan, a clear "prove it" project, and notes. You learn by shipping.

## Who this is for

- Software engineers who know backends (Django, FastAPI, PostgreSQL) and want real geospatial skill
- People aiming at cocoa / agri / EUDR-style plot compliance systems (especially in Ghana and West Africa)
- Self-learners who prefer one main free resource per phase, then a concrete deliverable

## How to use this repo

1. Read [`ROADMAP.md`](./ROADMAP.md) for the big picture, EUDR context and the full checklist.
2. Open the phase you are on, for example [`phase-1/PLAN.md`](./phase-1/PLAN.md), and work week by week.
3. Keep personal notes in `notes/` (one file per phase).
4. Tick checkboxes as you go (`- [ ]` → `- [x]`).
5. Ship each "Prove it" project before you move on.

**Pace:** about 8–10 hours per week (~26 weeks / 6 months). The deliverable matters more than the calendar.

**Time split:** ~40% learning, ~50% building, ~10% notes.

## Roadmap at a glance

| Phase | Weeks | Topic | Prove-it project |
| ----- | ----- | ----- | ---------------- |
| 0 | 0 | Setup and orientation | Working local GIS toolbox |
| 1 | 1–3 | GIS and geodesy foundations (QGIS) | Ghana cocoa-region map + CRS cheat sheet |
| 2 | 4–6 | Geospatial Python | `plotcheck`: EUDR plot-validator CLI |
| 3 | 7–9 | Advanced PostGIS | Overlap and forest-reserve conflict queries |
| 4 | 10–13 | Remote sensing and raster | Deforestation-since-2020 checker |
| 5 | 14–15 | Field data collection | Farm/nursery survey → PostGIS pipeline |
| 6 | 16–18 | Geospatial backends and standards | Vector tiles + OGC API on Asase GIS |
| 7 | 19–20 | Modern web mapping | MapLibre plot editor and dashboard |
| 8 | 21–23 | Production, scale and cloud-native | Deployed app, jobs, COGs on S3 |
| 9 | 24–26 | Capstone and career | "Asase Trace" v1.0 + write-up |

Detailed plans live in each phase folder:

```text
phase-0/ … phase-9/
  PLAN.md          ← week-by-week checklist for that phase
```

## Repo layout

```text
.
├── README.md              ← you are here
├── ROADMAP.md             ← full curriculum and checklists
├── ROADMAP.pdf            ← printable snapshot (may lag behind the .md)
├── notes/                 ← learning notes (glossary, cheatsheets)
├── phase-0/               ← Docker PostGIS, early setup
├── phase-1/               ← QGIS foundations
│   ├── PLAN.md
│   ├── course/            ← your QGIS project files (committed)
│   ├── data/              ← downloads (gitignored; fetch yourself)
│   └── exports/           ← map PDFs and outputs
├── phase-2/ … phase-9/    ← plans (and later code / artifacts)
└── .gitignore
```

## Datasets are not in this repo

Large and third-party datasets stay **out of git**. Each `PLAN.md` links to where to download them (course packs, HDX Ghana boundaries, Geofabrik, Copernicus, and so on). Put downloads under `phase-N/data/`.

## Threading project: Asase Trace

Most later phases add features to **Asase GIS** (GeoDjango + PostGIS + Leaflet), growing it into a cocoa farm-plot compliance and monitoring platform.

> **Never put real farmer personal data in public repos.** Use synthetic or open data for portfolio work. Company data stays inside company systems.

## Progress so far

| Phase | Status |
| ----- | ------ |
| 0 Setup | Mostly done (QGIS, Python geo env, PostGIS, Earth Engine, notes folder) |
| 1 Foundations | In progress — Spatial Thoughts QGIS course (section 1.1+) |
| 2–9 | Not started |

## Licence and attribution

- This roadmap and your notes: add a licence when you publish the LinkedIn post (suggested: MIT for text/plans you authored).
- Third-party courses and data keep their own licences (Spatial Thoughts, Natural Earth, OSM / ODbL, Copernicus, Hansen, and so on). Always credit them in READMEs.

## Author

**Blessing Edmund Kwame Dogbe** · [@GeekKwame](https://github.com/GeekKwame)

If this guide helps you, star the repo and share it. When the full path is finished, the LinkedIn announcement will point here.
