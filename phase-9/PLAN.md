# Phase 9 plan: Capstone and career

**Goal:** Combine everything into one polished, documented system, "Asase Trace" v1.0, and use it to show what you can do.

```text
Field (QField / Kobo)  →  Ingest + plotcheck validation  →  PostGIS (plots, nurseries, reserves, audit)
        →  forestcheck (Sentinel-2 / Hansen / JRC)  →  Risk scores
        →  APIs (DRF-GIS, OGC API Features, vector tiles, TiTiler)
        →  MapLibre web app + EUDR GeoJSON / GeoParquet exports
        →  Docker / Terraform / GitHub Actions on AWS
```

## Part 1: Integrate and polish

- [ ] Run the full pipeline end to end with synthetic data: field form → ingest → validation → risk check → map → export
- [ ] Fix the rough edges you find
- [ ] README:
  - [ ] Architecture diagram
  - [ ] Data sources and their licences
  - [ ] CRS decisions (what is stored in which CRS, and why)
  - [ ] Limitations (pixel size, clouds, shaded cocoa, GPS accuracy under canopy)
  - [ ] Screenshots or a GIF

## Part 2: Show it

- [ ] Record a 3-minute demo video
- [ ] Write a blog post: *"Building an EUDR plot-compliance pipeline for Ghana cocoa with open-source GIS"*
- [ ] Update your portfolio:
  - [ ] Add a **"Geospatial"** group to `CAPABILITY_GROUPS` in `my-portfolio/src/components/Skills.jsx`
  - [ ] Add Asase Trace to `src/data/projects.js`

## Part 3: Share it

- [ ] Give a **lunch-and-learn at Afarinick** on what you built and how it could apply internally
- [ ] Go through "Concepts you must be able to explain without notes" in `ROADMAP.md`, and explain each one out loud in 2 minutes
- [ ] Fill in the progress log in `ROADMAP.md`
- [ ] Pick one optional specialisation:
  - **Geo-AI:** land-cover classification and cocoa/shade-tree detection with [TorchGeo](https://torchgeo.readthedocs.io/en/stable/) and [segment-geospatial](https://samgeo.gishub.org/)
  - **QGIS plugins:** internal tools for Afarinick's GIS team ([PyQGIS Developer Cookbook](https://docs.qgis.org/latest/en/docs/pyqgis_developer_cookbook/))
  - **Routing and logistics:** nursery-to-farm seedling distribution with [pgRouting](https://docs.pgrouting.org/)
  - **Big open data:** [Overture Maps](https://overturemaps.org/) and [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/docs/overview/about/)

## Ongoing (from Phase 1 onwards, not just now)

- [ ] Map Ghana on OpenStreetMap: [LearnOSM](https://learnosm.org/en/) → [HOT Tasking Manager](https://tasks.hotosm.org/)
- [ ] Join [YouthMappers](https://www.youthmappers.org/) and [OSGeo](https://www.osgeo.org/)
- [ ] Answer one question a week on [GIS StackExchange](https://gis.stackexchange.com/)
- [ ] Make one open-source contribution (docs or a bug fix) to [GeoPandas](https://github.com/geopandas/geopandas), [django-rest-framework-gis](https://github.com/openwisp/django-rest-framework-gis) or the [opengeos](https://github.com/opengeos) tools
- [ ] Aim to give a talk at [FOSS4G](https://foss4g.org/) or a local meetup within 12 months

## Notes

- Write `notes/09-capstone.md`: what you learned, one question, one limitation

## Done when

- [ ] Asase Trace v1.0 is deployed, documented and in your portfolio
- [ ] The demo video and blog post are published
- [ ] You've presented it at Afarinick
