# Phase 5 plan: Field data collection (Weeks 14–15)

**Goal:** Afarinick's data starts in the field, with officers walking farm boundaries and recording nurseries. Learn how that data is captured, so your backend can accept it cleanly.

**Main resource (⭐):** [QField docs, "My first project"](https://docs.qfield.org/get-started/tutorials/my-first-project/)
**Also:** [ODK XLSForm reference](https://docs.getodk.org/xlsform/), [KoboToolbox help centre](https://support.kobotoolbox.org/)

## Week 14: Field tools and forms

- [ ] **QField:** install it on your phone, follow "My first project", and take a QGIS project into the field offline
- [ ] **KoboToolbox:** create a free account and a test form
- [ ] **XLSForm:** learn the `survey` and `choices` sheets, and the `geopoint`, `geotrace` and `geoshape` question types
- [ ] Build two forms:
  - [ ] **Farm Plot Registration:** farmer code (not the name), crop, planting year, `geoshape` boundary, photo, GPS accuracy
  - [ ] **Nursery Batch:** location, species, seedling count, sowing and dispatch dates
- [ ] GPS accuracy:
  - Phone GPS (±5–15 m, worse under cocoa canopy) vs RTK (centimetres)
  - Filter points by their reported accuracy, and average repeated readings
- [ ] Data protection: consent, collecting only what you need, and keeping personal data out of public repos
- [ ] **At work:** ask which tool Afarinick's field officers actually use, and look at a real form if you're allowed

## Week 15: Walk a boundary and build the ingest (Prove it)

- [ ] Walk the boundary of a real open space (a park or school field) with QField or KoboCollect
- [ ] Compare the walked area with the same shape traced on satellite imagery. How far off was it?
- [ ] Write an ingest job in Asase GIS (`manage.py ingest_kobo` or a Celery task) that:
  - [ ] Pulls new submissions from the Kobo API (or ODK Central API)
  - [ ] Runs each one through `plotcheck`
  - [ ] Loads valid plots into PostGIS
  - [ ] Flags bad records for review instead of silently dropping them
  - [ ] Uses the submission's unique ID, so running it twice doesn't create duplicates
- [ ] Tests using saved sample submissions (synthetic data only)

## Notes

- Write `notes/05-field-data.md`: what you learned, one question, one limitation

## Done when

- [ ] Both XLSForms work on a phone
- [ ] A walked boundary goes from phone → Kobo → `plotcheck` → PostGIS → visible in Asase GIS
- [ ] You can explain resolution vs accuracy vs precision (phone GPS under canopy vs a 10 m Sentinel-2 pixel)
