# Geospatial Software Engineer Roadmap — Edmund Dogbe

> Built for: **Blessing Edmund Kwame Dogbe**, Software Engineer at **Afarinick Company Limited** (Accra).
> Goal: go from "backend engineer who has built one GIS project" to "geospatial software engineer who can own Afarinick's farm, forest, and nursery mapping systems".
> Prepared: October 2026. Every link below was checked and was live when this was written.

---

## How to use this roadmap

1. **Go through the phases in order.** Each phase builds on the one before it. Don't skip ahead unless you can already deliver that phase's **"Prove it" project**.
2. **Pace:** about **8–10 hours per week**, which fits around a full-time job. At that pace the roadmap takes about **26 weeks (6 months)**. If a phase takes longer, that's fine; the deliverable matters more than the calendar.
3. **For each phase:**
  - Pick **one main resource** (marked ⭐) and work through it. Use the other resources only when you're stuck.
  - Watch the video only when the written material isn't clicking.
  - Ship the **"Prove it" project** to GitHub with a README before you move on.
  - Tick the checkboxes as you go (`- [ ]` → `- [x]`).
4. **Time split:** about 40% learning, 50% building, 10% writing notes. Your notes go in `notes/` in this folder (one file per phase).
5. **One project runs through the whole roadmap.** Most phases add a feature to **Asase GIS** (your existing GeoDjango + PostGIS + Leaflet project). By the end it becomes a **cocoa farm-plot compliance and monitoring platform**, the kind of system Afarinick's work needs.

> **Never use real Afarinick farmer data in public repos.** Farmer names, plot boundaries and phone numbers are personal data. Use synthetic data or open datasets for your portfolio, and use company data only inside company systems.

---



## Where you're starting from

Based on your CV, portfolio and Asase GIS:


| Area           | You already have                                        | Gap to close                                                                                    |
| -------------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Backend        | Django, DRF, FastAPI, Pydantic, SQLAlchemy, REST design | GeoDjango beyond the basics, OGC standards, tile serving                                        |
| Databases      | PostgreSQL, PostGIS basics, schema design               | Spatial indexing, query plans, validity, topology, geography vs geometry                        |
| GIS concepts   | GeoJSON, EPSG:4326, area in UTM 30N                     | Datums, Ghana's coordinate systems, raster data, cartography, QGIS fluency                      |
| Python data    | Pandas, scikit-learn                                    | GeoPandas, Shapely 2, pyproj, rasterio, xarray                                                  |
| Frontend maps  | Leaflet                                                 | MapLibre GL JS, vector tiles, drawing/editing polygons                                          |
| Remote sensing | None                                                    | Sentinel-2, NDVI, Earth Engine, forest-loss datasets                                            |
| Field data     | None                                                    | QField, ODK/KoboToolbox, GPS accuracy, offline sync                                             |
| DevOps/Cloud   | Docker, GitHub Actions, AWS, Terraform                  | GDAL in containers, Cloud Optimized GeoTIFFs (COGs) on S3, background jobs for heavy processing |
| Maths          | BSc Applied Mathematics                                 | You already have the maths for projections and geodesy. Use it.                                 |


**Your edge:** Most GIS people can't write production backends, and most backend engineers don't understand coordinate systems. You're close to being both, and that combination is rare.

---



## Why this matters at Afarinick: the EUDR

Afarinick works on cocoa rehabilitation, nurseries and GIS mapping. The biggest geospatial requirement in the Ghana cocoa sector right now is the **EU Deforestation Regulation (EUDR)**:

- It **applies from 30 December 2026** to large and medium operators, and from 30 June 2027 to micro and small operators.
- Every cocoa batch sold into the EU must be traceable to the **geolocation of every plot** it came from:
  - plots **over 4 ha** need a **polygon**
  - plots under 4 ha can use a point
  - coordinates must be **WGS 84 (EPSG:4326)** with **6 decimal places**
- Plots must be **deforestation-free since 31 December 2020** and legal. For example, a farm can't be inside a forest reserve unless it is an admitted farm.
- The EU system takes **GeoJSON**. It rejects polygons with holes, self-intersecting ("figure-eight") shapes and unclosed rings.
- COCOBOD is building the **Ghana Cocoa Traceability System**, including a deforestation-risk module.

This is mostly a software problem: data collection, validation, storage, satellite checks, APIs and reporting. **That's why the project in this roadmap is built around it.**

Read these first (about 1 hour):

- [EU Commission: Regulation on deforestation-free products](https://environment.ec.europa.eu/topics/forests/deforestation/regulation-deforestation-free-products_en)
- [EUDR Information System: GeoJSON file rules](https://eudr.webcloud.ec.europa.eu/tracesnt/help/eudr-documentation/operator/geojson-description.html) → the spec your validator will implement
- [EFI Cocoa Insight: The role of spatial information for EUDR (PDF)](https://zerodeforestationhub.eu/wp-content/uploads/2025/10/EFI-Cocoa-Insight-1-EN-v2-1.pdf)
- [EFI: EUDR preparedness check of Ghana (PDF, 2026)](https://cocoa.efi.int/wp-content/uploads/2026/04/EUDR-Preparedness-check-of-Ghana.pdf)

---



## Roadmap at a glance


| Phase | Weeks   | Topic                              | Prove-it project                                      |
| ----- | ------- | ---------------------------------- | ----------------------------------------------------- |
| 0     | 0       | Setup and orientation              | Working local GIS toolbox                             |
| 1     | 1–3     | GIS and geodesy foundations (QGIS) | Ghana cocoa-region map plus a CRS cheat sheet         |
| 2     | 4–6     | Geospatial Python                  | `plotcheck`: an EUDR plot-validator command-line tool |
| 3     | 7–9     | Advanced PostGIS                   | Overlap and forest-reserve conflict queries           |
| 4     | 10–13   | Remote sensing and raster data     | Deforestation-since-2020 checker                      |
| 5     | 14–15   | Field data collection              | Farm/nursery survey form → PostGIS pipeline           |
| 6     | 16–18   | Geospatial backends and standards  | Vector tiles plus an OGC API on Asase GIS             |
| 7     | 19–20   | Modern web mapping                 | MapLibre plot editor and dashboard                    |
| 8     | 21–23   | Production, scale and cloud-native | Deployed, monitored, background jobs, COGs on S3      |
| 9     | 24–26   | Capstone and career                | "Asase Trace" v1.0 plus a write-up and talk           |
| 🌐    | Ongoing | Community and open source          | OSM Ghana, FOSS4G, contributions                      |


---



## Phase 0: Setup and orientation (Week 0, about 4 hours)

**Goal:** Get every tool installed now, so later phases are spent learning rather than fixing installs.

- [x] Install **QGIS (LTR version)**: [qgis.org/download](https://www.qgis.org/download/)
- [x] Create a Python geospatial environment with conda-forge or `uv` that includes `geopandas shapely pyproj pyogrio rasterio rioxarray xarray pystac-client jupyterlab folium leafmap`
- [x] Run PostGIS in Docker (you already have a Compose file in Asase GIS) and install the GDAL CLI (`ogr2ogr`, `gdalinfo`)
- [x] Sign up for **Google Earth Engine** for noncommercial/learning use: [earthengine.google.com/noncommercial](https://earthengine.google.com/noncommercial/). If you use it for Afarinick work, check the [commercial pricing](https://cloud.google.com/earth-engine/pricing).
- [x] Create a **Copernicus Data Space** account: [dataspace.copernicus.eu](https://dataspace.copernicus.eu/)
- [x] Create `notes/` in this folder and start `notes/00-glossary.md`
- [ ] **At work:** ask your manager or IT lead which GIS tools, data formats and coordinate systems Afarinick already uses (for example QGIS/ArcGIS, KoboToolbox/ODK, shapefiles/KML). Write the answers down, because they'll shape what you emphasise later.

**Bookmark:**

- [GIS StackExchange](https://gis.stackexchange.com/): the Stack Overflow of GIS
- [Awesome Geospatial](https://github.com/sacridini/Awesome-Geospatial): a big list of tools
- [epsg.io](https://epsg.io/32630): look up any coordinate reference system

---



## Phase 1: GIS and geodesy foundations (Weeks 1–3)

**Goal:** Think like a GIS analyst. Most "GIS bugs" in software are really misunderstood concepts: the wrong CRS, swapped lat/lon, invalid geometry, or area measured in degrees.

### Learn

- [ ] Vector vs raster data, layers, attributes, symbology
- [ ] **Datum vs projection vs CRS**; geographic vs projected coordinates; what an EPSG code is
- [ ] **Ghana's coordinate systems:**
  - [EPSG:4326 (WGS 84)](https://epsg.io/4326): GPS and GeoJSON
  - [EPSG:32630 (UTM 30N)](https://epsg.io/32630): metric work in most of Ghana
  - [EPSG:2136 (Accra / Ghana National Grid)](https://epsg.io/2136) and [EPSG:25000 (Leigon / Ghana Metre Grid)](https://epsg.io/25000): the legacy systems used on older Ghana survey and forest-reserve maps
- [ ] Why area and distance need a projected CRS or geodesic maths. (Ghana sits across UTM 30N and 31N, so know when that matters.)
- [ ] Geometry validity: rings, orientation, self-intersections, slivers, gaps, overlaps
- [ ] File formats: GeoJSON ([RFC 7946](https://datatracker.ietf.org/doc/html/rfc7946), longitude before latitude), Shapefile and its limits, **GeoPackage** (the modern default), KML, GeoTIFF
- [ ] Spatial analysis basics: buffer, clip, intersect, dissolve, spatial join, zonal statistics
- [ ] Cartography: map layouts, legends, scale, choropleths



### Resources

- ⭐ **Spatial Thoughts: Introduction to QGIS (free full course, data, and video):** [courses.spatialthoughts.com/introduction-to-qgis.html](https://courses.spatialthoughts.com/introduction-to-qgis.html)
- 📖 [QGIS Training Manual (official)](https://docs.qgis.org/latest/en/docs/training_manual/) and the [QGIS User Manual](https://docs.qgis.org/latest/en/docs/user_manual/)
- 📖 [QGIS Tutorials and Tips by Ujaval Gandhi](https://www.qgistutorials.com/en/)
- 📖 [USGS: *Map Projections: A Working Manual* (Snyder), free PDF](https://pubs.usgs.gov/publication/pp1395). Your maths degree makes this readable; do chapters 1–8.
- 🎥 [Matt Forrest: Learn GIS, QGIS Full Course for Beginners](https://www.youtube.com/watch?v=SovdBaus7pM)
- 🎥 [Playlist: Complete QGIS Training Manual, beginner to advanced (v3.40)](https://www.youtube.com/playlist?list=PLX50j2HV43tdkUIiXMMWkGquWh_5I058S)
- 📺 Channels: [Spatial Thoughts](https://www.youtube.com/@spatialthoughts) · [Klas Karlsson (QGIS)](https://www.youtube.com/@KlasKarlsson) · [GeoDelta Labs](https://www.youtube.com/@GeoDeltaLabs) · [GIS Geography](https://www.youtube.com/@GISGeography)



### Ghana data to practise with

- [HDX: Ghana administrative boundaries (regions/districts)](https://data.humdata.org/dataset/cod-ab-gha)
- [geoBoundaries](https://www.geoboundaries.org/) (an alternative boundary source)
- [Geofabrik: OpenStreetMap extract for Ghana](https://download.geofabrik.de/africa/ghana.html)
- [Google Open Buildings](https://sites.research.google/open-buildings/) (covers Ghana)
- [Global Forest Watch](https://www.globalforestwatch.org/): browse tree-cover loss in the Western, Ashanti and Eastern cocoa belts



### 🎯 Prove it

**"Ghana Cocoa Belt" QGIS project.** It should contain regions and districts, OSM roads and settlements, forest-loss tiles from GFW, and about 20 hand-digitised synthetic "farm" polygons. Then:

1. Reproject everything to UTM 30N and calculate areas.
2. Deliberately create 3 invalid polygons and fix them with *Check Validity* / *Fix Geometries*.
3. Export a print layout to PDF.
4. Write `notes/01-crs-cheatsheet.md`: which CRS to use for what in Ghana, and why.

---



## Phase 2: Geospatial Python (Weeks 4–6)

**Goal:** Do everything you did in QGIS, but in reproducible, testable Python.

### Learn

- [ ] **GeoPandas:** read/write (with the `pyogrio` engine), `to_crs`, `sjoin`, `overlay`, `dissolve`, `clip`, `.area`, `.buffer`
- [ ] **Shapely 2.x:** vectorised operations, `make_valid`, `is_valid_reason`, `set_precision`, predicates (`intersects`, `within`, `covers`), STRtree spatial index
- [ ] **pyproj:** `Transformer`, `always_xy=True` (the lat/lon order trap), geodesic area with `Geod`
- [ ] **GDAL/OGR CLI:** `ogrinfo`, `ogr2ogr` (format conversion, reprojection, SQL filters), `gdalinfo`
- [ ] Handling messy real-world inputs: KML from phones, CSVs of GPS points, mixed CRS, duplicate vertices, 3D coordinates



### Resources

- ⭐ **Spatial Thoughts: Python Foundation for Spatial Analysis (free full course and video playlist):** [courses.spatialthoughts.com/python-foundation.html](https://courses.spatialthoughts.com/python-foundation.html)
- 📖 [Automating GIS Processes (University of Helsinki)](https://autogis-site.readthedocs.io/en/latest/): excellent free course
- 📖 [Introduction to Python for Geographic Data Analysis (free book)](https://pythongis.org/)
- 📖 [Geocomputation with Python (free book)](https://py.geocompx.org/)
- 📖 [Qiusheng Wu: Introduction to GIS Programming (free course site)](https://geog-312.gishub.org/)
- 📚 Docs: [GeoPandas user guide](https://geopandas.org/en/stable/docs/user_guide.html) · [Shapely manual](https://shapely.readthedocs.io/en/stable/manual.html) · [pyproj](https://pyproj4.github.io/pyproj/stable/) · [pyogrio](https://pyogrio.readthedocs.io/en/latest/) · [GDAL programs](https://gdal.org/en/stable/programs/index.html)
- 🎥 [Matt Forrest: Geospatial Python, Full Course for Beginners with GeoPandas](https://www.youtube.com/watch?v=0mWgVVH_dos)
- 🎥 [Playlist: Introduction to GIS Programming (Qiusheng Wu, full university lectures)](https://www.youtube.com/playlist?list=PLAxJ4-o7ZoPfb18kNe2luWX9xKg1233i9)
- 📺 Channel: [Open Geospatial Solutions (Qiusheng Wu)](https://www.youtube.com/@giswqs)



### 🎯 Prove it

`plotcheck`**: an EUDR plot-validator command-line tool and Python package** (new repo, with tests and CI). It takes GeoJSON, KML, GPKG or CSV and:

1. Normalises everything to EPSG:4326, longitude before latitude, rounded to 6 decimal places.
2. Flags or fixes: unclosed rings, self-intersections, holes (split them, following EUDR guidance), duplicate vertices, slivers, and plots that are suspiciously tiny or huge.
3. Calculates area in hectares (UTM 30N **and** geodesic, and reports the difference).
4. Enforces "> 4 ha must be a polygon".
5. Detects **overlaps between plots** using an STRtree index.
6. Outputs a cleaned EUDR-style GeoJSON plus a CSV/HTML error report.

Write pytest tests with hand-crafted bad geometries. This will be directly useful at work.

---



## Phase 3: Advanced PostGIS (Weeks 7–9)

**Goal:** Move from "PostGIS stores my polygons" to "I can design, query, index and tune a spatial database of a million farm plots".

### Learn

- [ ] `geometry` vs `geography`, and when to use each; SRIDs and type modifiers (`geometry(MultiPolygon, 4326)`)
- [ ] **GiST indexes**, `EXPLAIN ANALYZE`, the `&&` bounding-box operator, why `ST_DWithin` beats `ST_Distance < x`
- [ ] `ST_MakeValid`, `ST_IsValidReason`, `ST_SnapToGrid`, `ST_ReducePrecision`
- [ ] Spatial joins at scale; `ST_Subdivide` for big polygons such as forest reserves
- [ ] Nearest-neighbour queries with `<->` (KNN)
- [ ] Overlap detection between plots (self-join plus `ST_Intersection` area)
- [ ] Edit history and audit trails with triggers (who moved a farm boundary, and when)
- [ ] Loading data: `ogr2ogr` → PostGIS, `shp2pgsql`, `COPY`
- [ ] Optional: PostGIS raster, topology, [pgRouting](https://docs.pgrouting.org/)



### Resources

- ⭐ **Official PostGIS workshop (do every module, including Validity, Indexing, Geography, Nearest-Neighbour and Tracking Edit History):** [postgis.net/workshops/postgis-intro](https://postgis.net/workshops/postgis-intro/)
- 📖 [PostGIS reference docs](https://postgis.net/docs/), for example [ST_MakeValid](https://postgis.net/docs/ST_MakeValid.html)
- 📖 [Crunchy Data interactive PostGIS tutorials (run in the browser)](https://www.crunchydata.com/developers/tutorials)
- 📖 [Paul Ramsey's blog (PostGIS co-founder)](https://blog.cleverelephant.ca/): performance deep-dives
- 📖 [GeoDjango database API](https://docs.djangoproject.com/en/stable/ref/contrib/gis/db-api/): map each SQL concept to its ORM equivalent
- 🎥 [Playlist: Spatial Data Management with PostGIS (12 videos, about 5 hours)](https://www.youtube.com/playlist?list=PLAxJ4-o7ZoPcvp0ETujkLVCmKIGj-YvlG)
- 🎥 [PostGIS for Newbies (Elizabeth Christensen, PostgreSQL Europe)](https://www.youtube.com/watch?v=vmbNpre02hk)
- 📺 Channel: [Crunchy Data](https://www.youtube.com/@CrunchyData)



### 🎯 Prove it

**Add to Asase GIS:**

1. A `ForestReserve` / `ProtectedArea` model. Use synthetic shapes, or open protected-area data if the licence allows.
2. Endpoints: `/api/plots/{id}/conflicts/` (overlapping plots and reserve intersections, with overlap area in hectares) and `/api/plots/nearby/?lat=&lon=&radius_m=`.
3. Seed **100,000 synthetic plots**, then show `EXPLAIN ANALYZE` before and after the GiST index and `ST_Subdivide`, and record the timings in the README.
4. An audit trigger or `django-simple-history` table for boundary edits.
5. `docs/queries.sql`: your 15 best spatial queries, each with a comment explaining it.

---



## Phase 4: Remote sensing and raster data (Weeks 10–13)

**Goal:** Answer the question at the centre of the EUDR: **"Has this plot lost forest since 31 December 2020?"** You'll also be able to monitor rehabilitated cocoa farms and nursery out-planting with satellite data.

### Learn

- [ ] Raster basics: bands, resolution, nodata, data types, affine transform, CRS
- [ ] **Satellites:** Sentinel-2 (10 m, every 5 days, free), Landsat (30 m, archive back to the 1980s), and why clouds are a big problem over Ghana's forest zone (and why Sentinel-1 radar helps)
- [ ] Spectral indices: **NDVI**, NDMI; cloud masking with the Sentinel-2 SCL band
- [ ] **rasterio** (read/write/window/reproject/mask), **rioxarray** + **xarray** (stacks of images over time)
- [ ] **Cloud-native geospatial:** COG, **STAC** catalogues, `pystac-client`, `odc-stac` / `stackstac`
- [ ] **Google Earth Engine** (JavaScript Code Editor plus the Python API and `geemap`)
- [ ] Forest datasets relevant to the EUDR:
  - [Hansen Global Forest Change (GLAD/UMD)](https://glad.earthengine.app/view/global-forest-change) ([in Earth Engine](https://developers.google.com/earth-engine/datasets/catalog/UMD_hansen_global_forest_change_2024_v1_12))
  - [JRC Global Forest Cover 2020 (the EU's reference map)](https://forobs.jrc.ec.europa.eu/GFC) ([in Earth Engine](https://developers.google.com/earth-engine/datasets/catalog/JRC_GFC2020_V2))
  - [FAO Open Foris **Whisp](https://openforis.org/solutions/whisp/)**: an open-source deforestation-risk tool built for the EUDR. Study how it works.
- [ ] Zonal statistics: summarising raster pixels inside each farm polygon



### Resources

- ⭐ **Spatial Thoughts: End-to-End Google Earth Engine (free full course and videos):** [courses.spatialthoughts.com/end-to-end-gee.html](https://courses.spatialthoughts.com/end-to-end-gee.html)
  - 🎥 [Module 1: Earth Engine Basics (video)](https://www.youtube.com/watch?v=daYhxVVIpJU)
- ⭐ **Digital Earth Africa training (free, Africa-focused, includes a Ghana-relevant sandbox):** [training.digitalearthafrica.org](https://training.digitalearthafrica.org/) · [DE Africa docs and sandbox](https://docs.digitalearthafrica.org/en/latest/sandbox/index.html)
- 📖 [Spatial Thoughts: Python for Remote Sensing](https://courses.spatialthoughts.com/python-remote-sensing.html) and the [GDAL Tools course](https://courses.spatialthoughts.com/gdal-tools.html)
- 📖 [Qiusheng Wu: Advanced Geospatial Programming (GEOG 414)](https://geog-414.gishub.org/) and the free book [Earth Engine and Geemap](https://book.geemap.org/)
- 📚 Docs: [rasterio](https://rasterio.readthedocs.io/en/stable/) · [rioxarray](https://github.com/corteva/rioxarray) · [xarray](https://docs.xarray.dev/en/stable/) · [pystac-client](https://pystac-client.readthedocs.io/en/stable/) · [odc-stac](https://odc-stac.readthedocs.io/) · [geemap](https://geemap.org/) · [Earth Engine guides](https://developers.google.com/earth-engine/guides)
- 📖 [STAC spec](https://stacspec.org/en) · [STAC Index](https://stacindex.org/) · [Planetary Computer: reading STAC](https://planetarycomputer.microsoft.com/docs/quickstarts/reading-stac/) · [Earth Search (Sentinel-2 on AWS)](https://element84.com/earth-search/) · [Cloud-Native Geospatial Guide](https://guide.cloudnativegeo.org/)
- 📖 [Sentinel-2 mission guide](https://sentiwiki.copernicus.eu/web/s2-mission) · [Copernicus Browser](https://browser.dataspace.copernicus.eu/) · [Sentinel Hub custom scripts (index recipes)](https://custom-scripts.sentinel-hub.com/)
- 📖 [NASA ARSET free remote-sensing trainings](https://appliedsciences.nasa.gov/what-we-do/capacity-building/arset)
- 🎥 [Playlist: Google Earth Engine and geemap Python tutorials](https://www.youtube.com/playlist?list=PLAxJ4-o7ZoPccOFv1dCwvGI6TYnirRTg3)
- 🎥 [geemap and Earth Engine in Google Colab](https://www.youtube.com/watch?v=fG6kx9vq7hs)
- 🎥 [Sentinel-2 in QGIS: band combinations, NDVI, raster calculator](https://www.youtube.com/watch?v=A99pMv4CFWg)
- 📺 Channel: [Digital Earth Africa](https://www.youtube.com/@DigitalEarthAfrica/playlists)



### 🎯 Prove it

`forestcheck`**, an EUDR deforestation checker.** It can live inside Asase GIS as a module or stand alone. For each plot polygon:

1. Was the plot forest on 31 December 2020 (JRC GFC2020)?
2. How much tree-cover loss has there been since 2021 (Hansen)?
3. A Sentinel-2 NDVI time series from 2020 to now (via STAC or Earth Engine).
4. Output a **risk flag** (low/medium/high) with an explanation, plus a PNG/HTML "plot report card".
5. Bonus: for rehabilitation plots, show NDVI recovery after replanting.

Be clear about the limits: 10–30 m pixels, cloud cover, and the fact that cocoa under shade trees is hard to tell apart from forest. A good README section on limitations makes you look senior.

---



## Phase 5: Field data collection (Weeks 14–15)

**Goal:** Afarinick's data starts in the field, with officers walking farm boundaries and recording nurseries. Learn how that data is captured, so your backend can accept it cleanly.

### Learn

- [ ] **QField** (mobile app for QGIS projects; offline; polygon digitising by walking the boundary)
- [ ] **ODK / KoboToolbox** and **XLSForm** (`geopoint`, `geotrace`, `geoshape` question types)
- [ ] GPS accuracy: phone GPS vs RTK, canopy error under cocoa, filtering points by accuracy, averaging
- [ ] Offline-first sync, conflict resolution, unique IDs from the device
- [ ] Pulling submissions from the Kobo/ODK Central APIs into PostGIS (scheduled ingest)
- [ ] Data protection when collecting farmer personal data (consent, minimal collection)



### Resources

- ⭐ **QField docs, "My first project":** [docs.qfield.org/get-started/tutorials/my-first-project](https://docs.qfield.org/get-started/tutorials/my-first-project/) · [QField docs home](https://docs.qfield.org/)
- 📖 [ODK docs](https://docs.getodk.org/) · [ODK Central intro](https://docs.getodk.org/central-intro/) · [ODK XLSForm reference](https://docs.getodk.org/xlsform/) · [XLSForm.org](https://xlsform.org/en/)
- 📖 [KoboToolbox help centre](https://support.kobotoolbox.org/)
- 📖 [Mergin Maps docs](https://merginmaps.com/docs/) (an alternative QGIS-based field app)
- 🎥 [QGIS: Introducing QField](https://www.youtube.com/watch?v=sVLlTu9evfM)
- 🎥 [Seamless fieldwork with QField and QFieldCloud (Marco Bernasocchi)](https://www.youtube.com/watch?v=h58EzJR7XwI)



### 🎯 Prove it

1. Build an **XLSForm** for "Farm Plot Registration" (farmer code, crop, planting year, `geoshape` boundary, photo, GPS accuracy) and one for "Nursery Batch" (location, species, seedling count, dates).
2. Walk the boundary of a real open space (a park or school field) with QField or KoboCollect.
3. Write an ingest job (`manage.py ingest_kobo` or a Celery task) that pulls submissions → runs them through `plotcheck` → loads them into Asase GIS → flags bad records for review.

---



## Phase 6: Geospatial backends and standards (Weeks 16–18)

**Goal:** Serve spatial data the way professional systems do: fast vector tiles, standard OGC APIs, and dynamic raster tiles.

### Learn

- [ ] GeoDjango in depth: `GEOSGeometry`, spatial lookups, `Transform`, `Area`, custom `Func` wrappers for `ST_*` functions, GIS admin widgets
- [ ] `djangorestframework-gis`: `GeoFeatureModelSerializer`, bbox filters, pagination of FeatureCollections
- [ ] The FastAPI + GeoAlchemy2 alternative (you already know FastAPI)
- [ ] **OGC standards:** WMS/WFS (legacy but everywhere), **OGC API – Features** (the modern REST equivalent)
- [ ] **Vector tiles (MVT):** `ST_AsMVT`, `/z/x/y` tile maths, tile servers (**Martin**, pg_tileserv), static **PMTiles**, `tippecanoe`
- [ ] **Dynamic raster tiles** from COGs (TiTiler)
- [ ] GeoServer basics, because many government and NGO partners use it



### Resources

- ⭐ **pygeoapi workshop, "Diving into pygeoapi" (OGC APIs in Python):** [dive.pygeoapi.io](https://dive.pygeoapi.io/)
- 📖 [GeoDjango tutorial](https://docs.djangoproject.com/en/stable/ref/contrib/gis/tutorial/) · [GeoDjango reference](https://docs.djangoproject.com/en/stable/ref/contrib/gis/) · [django-rest-framework-gis](https://github.com/openwisp/django-rest-framework-gis)
- 📖 [GeoAlchemy2](https://geoalchemy-2.readthedocs.io/en/latest/) · [FastAPI tutorial](https://fastapi.tiangolo.com/tutorial/)
- 📖 [OGC API – Features](https://ogcapi.ogc.org/features/) · [OGC standards list](https://www.ogc.org/standards/)
- 📖 [Martin tile server](https://maplibre.org/martin/) ([using it with MapLibre](https://maplibre.org/martin/using-with-maplibre/)) · [pg_tileserv](https://github.com/CrunchyData/pg_tileserv) · [pg_featureserv](https://github.com/CrunchyData/pg_featureserv)
- 📖 [Protomaps / PMTiles](https://docs.protomaps.com/) · [tippecanoe](https://github.com/felt/tippecanoe) · [TiTiler](https://developmentseed.org/titiler/)
- 📖 [GeoServer user manual: getting started](https://docs.geoserver.org/latest/en/user/gettingstarted/index.html)
- 🎥 [Maps with GeoDjango, PostGIS and Leaflet (DjangoCon Europe talk)](https://djangotv.com/videos/djangocon-europe/2019/djangocon-2019-maps-with-geodjango-postgis-and-leaflet/)
- 🎥 [How to visualise millions of features: vector tiles, PostGIS and MapLibre](https://www.youtube.com/watch?v=ifkl30N-_-w)



### 🎯 Prove it

**Add to Asase GIS:**

1. Martin (or a Django `ST_AsMVT` view) serving your 100k plots as vector tiles.
2. An OGC API – Features endpoint via pygeoapi pointing at the same PostGIS database.
3. TiTiler serving your NDVI COGs from Phase 4.
4. Add all of these to `docker-compose.yml` and document each service in the README with an architecture diagram.

---



## Phase 7: Modern web mapping (Weeks 19–20)

**Goal:** Build map interfaces that field officers and managers actually want to use, and that can display 100k+ plots smoothly.

### Learn

- [ ] **MapLibre GL JS:** style spec, sources and layers, data-driven styling, feature-state for hover/selection, vector tile sources
- [ ] Drawing and editing polygons in the browser (Terra Draw, or Leaflet-Geoman in Leaflet), with snapping and validation feedback
- [ ] **Turf.js** for client-side geometry (area preview, overlap warnings before submit)
- [ ] OpenLayers (common in government and enterprise; know its basics)
- [ ] deck.gl / kepler.gl for big-data visualisation
- [ ] UX for maps: clustering, legends, filters, mobile layout, slow 3G networks in rural Ghana



### Resources

- ⭐ **MapLibre GL JS examples (work through 20+):** [maplibre.org/maplibre-gl-js/docs/examples](https://maplibre.org/maplibre-gl-js/docs/examples/) · [MapLibre style spec](https://maplibre.org/maplibre-style-spec/)
- 📖 [Leaflet examples](https://leafletjs.com/examples.html) · [Leaflet-Geoman](https://geoman.io/docs/leaflet) · [Terra Draw](https://terradraw.io/) · [Turf.js](https://turfjs.org/)
- 📖 [OpenLayers workshop](https://openlayers.org/workshop/en/)
- 📖 [deck.gl](https://deck.gl/) · [kepler.gl](https://kepler.gl/)
- 📖 [Spatial Thoughts: Mapping and Data Visualization with Python](https://courses.spatialthoughts.com/python-dataviz.html) · [leafmap](https://leafmap.org/) (quick dashboards)
- 🎥 [MapLibre tutorial: open-source vector map rendering](https://www.youtube.com/watch?v=aWCDIhe-fqM)



### 🎯 Prove it

**A React + MapLibre frontend for Asase GIS:**

1. A vector-tile layer of all plots, coloured by EUDR risk (from Phase 4).
2. Click a plot → side panel with attributes, NDVI chart and conflicts.
3. Draw/edit a plot → live area and overlap warnings with Turf → save via the API (server-side validation with `plotcheck`).
4. Filters by district, crop, risk and planting year; works on a phone.

---



## Phase 8: Production, scale and cloud-native (Weeks 21–23)

**Goal:** Use your DevOps and AWS strengths in a geospatial setting. This is where you can pull ahead of most GIS developers.

### Learn

- [ ] Docker images with GDAL that actually work ([official GDAL images](https://github.com/OSGeo/gdal/tree/master/docker)); pin versions of GDAL, PROJ and GEOS
- [ ] **Background jobs** for heavy geo work (Celery/RQ): imports, satellite checks, report generation
- [ ] Storing rasters as **COGs on S3** + CloudFront; vector tiles as **PMTiles** on S3 (serverless maps)
- [ ] **GeoParquet** + **DuckDB spatial** for analytics and exports outside PostGIS
- [ ] **H3** hexagonal indexing for aggregating plots into regional dashboards
- [ ] Testing geospatial code: geometry fixtures, property-based tests, snapshot GeoJSON, testing across CRS
- [ ] Observability: slow spatial query logging, tile cache hit rates
- [ ] Backup/restore of PostGIS; migrations that alter geometry columns safely
- [ ] Data licensing and attribution (OSM ODbL, Copernicus, Hansen CC-BY), and data protection for farmer data



### Resources

- ⭐ **Cloud-Native Geospatial Guide:** [guide.cloudnativegeo.org](https://guide.cloudnativegeo.org/)
- 📖 [COG](https://cogeo.org/) · [GeoParquet](https://geoparquet.org/) · [DuckDB spatial](https://duckdb.org/docs/stable/core_extensions/spatial/overview) · [H3](https://h3geo.org/)
- 📖 [Sentinel-2 COGs on AWS Open Data](https://registry.opendata.aws/sentinel-2-l2a-cogs/)
- 📖 [Celery docs](https://docs.celeryq.dev/) · [pytest-django](https://pytest-django.readthedocs.io/)
- 📖 [PostGIS workshop: tuning, security, backup and upgrades modules](https://postgis.net/workshops/postgis-intro/)
- 📺 Channel: [FOSS4G conference talks](https://www.youtube.com/@FOSS4G/videos). Search it for "COG", "STAC", "GeoParquet" and "vector tiles".
- 📺 Channel: [PyData talks](https://www.youtube.com/@PyDataTV). Search it for "geospatial".



### 🎯 Prove it

1. Deploy Asase GIS to AWS with Terraform (you've done this before), with PostGIS on RDS, COGs and PMTiles on S3 + CloudFront, and a Celery worker for satellite checks.
2. GitHub Actions: lint, run tests against a PostGIS service container, build the image, deploy.
3. A nightly export of all plots to **GeoParquet** plus an EUDR-format **GeoJSON** per cooperative/district.
4. An H3-aggregated "risk by district" dashboard view.

---



## Phase 9: Capstone and career (Weeks 24–26)



### 🏆 Capstone: "Asase Trace" v1.0

Combine everything into one polished, documented system:

```
Field (QField / Kobo)  →  Ingest + plotcheck validation  →  PostGIS (plots, nurseries, reserves, audit)
        →  forestcheck (Sentinel-2 / Hansen / JRC)  →  Risk scores
        →  APIs (DRF-GIS, OGC API Features, vector tiles, TiTiler)
        →  MapLibre web app + EUDR GeoJSON / GeoParquet exports
        →  Docker / Terraform / GitHub Actions on AWS
```

- [ ] A README with an architecture diagram, data sources and licences, CRS decisions, limitations, and screenshots/GIF
- [ ] A 3-minute demo video
- [ ] A blog post: *"Building an EUDR plot-compliance pipeline for Ghana cocoa with open-source GIS"*
- [ ] Update your portfolio: add a **"Geospatial"** group to `CAPABILITY_GROUPS` in `my-portfolio/src/components/Skills.jsx` and add the project to `src/data/projects.js`
- [ ] Offer a **lunch-and-learn at Afarinick** on what you built and how it could apply internally



### Optional specialisations (pick one after the capstone)

- **Geo-AI:** land-cover classification and cocoa/shade-tree detection with [TorchGeo](https://torchgeo.readthedocs.io/en/stable/), [segment-geospatial](https://samgeo.gishub.org/) and [scikit-learn](https://scikit-learn.org/stable/) (you already know ML)
- **QGIS plugin development:** build internal tools for Afarinick's GIS team with the [PyQGIS Developer Cookbook](https://docs.qgis.org/latest/en/docs/pyqgis_developer_cookbook/) ([plugin repository](https://plugins.qgis.org/))
- **Routing and logistics:** nursery-to-farm seedling distribution with [pgRouting](https://docs.pgrouting.org/)
- **Big open data:** [Overture Maps](https://overturemaps.org/) and [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/docs/overview/about/)

---



## Ongoing: community and open source (throughout)

- [ ] Map Ghana on OpenStreetMap: [LearnOSM](https://learnosm.org/en/) → [HOT Tasking Manager](https://tasks.hotosm.org/) → query OSM with [Overpass Turbo](https://overpass-turbo.eu/). [Ghana on OSM](https://www.openstreetmap.org/relation/192781).
- [ ] Join [YouthMappers](https://www.youthmappers.org/) (there are university chapters in Ghana) and [OSGeo](https://www.osgeo.org/)
- [ ] Watch talks from [FOSS4G](https://foss4g.org/) ([2026 edition](https://2026.foss4g.org/)); aim to give a talk at FOSS4G or a local meetup within 12 months
- [ ] Answer one question a week on [GIS StackExchange](https://gis.stackexchange.com/)
- [ ] Make one open-source contribution (docs or a bug fix) to [GeoPandas](https://github.com/geopandas/geopandas), [django-rest-framework-gis](https://github.com/openwisp/django-rest-framework-gis) or the [opengeos](https://github.com/opengeos) tools
- [ ] Follow: [Spatial Thoughts courses](https://spatialthoughts.com/courses/) · [Paul Ramsey](https://blog.cleverelephant.ca/) · [Matt Forrest](https://www.youtube.com/@MattForrest) · [Qiusheng Wu](https://www.youtube.com/@giswqs) · [Hatari Labs](https://www.youtube.com/@HatariLabs) · [Humanitarian OpenStreetMap Team](https://www.youtube.com/@HOTOSM)

---



## Concepts you must be able to explain without notes

Before calling yourself a geospatial engineer, explain each of these out loud in 2 minutes:

- [ ] Datum vs ellipsoid vs projection vs CRS; why GPS points don't line up with old Ghana National Grid maps
- [ ] Why `ST_Area` on EPSG:4326 geometry is meaningless, and three correct ways to get hectares
- [ ] GeoJSON coordinate order, and the libraries that use lat/lon instead (Leaflet's `LatLng`, many GPS CSVs)
- [ ] What makes a polygon invalid, and how `make_valid` can silently change what it means
- [ ] How a GiST index on geometries works (R-tree over bounding boxes), and why `ST_DWithin` uses it
- [ ] Vector tiles vs GeoJSON vs WMS: when to use each
- [ ] COG + STAC: why cloud-native formats let you read part of a satellite image without downloading all of it
- [ ] NDVI, and why it can't reliably tell shaded cocoa from forest
- [ ] EUDR geolocation rules (4 ha, 6 decimals, cut-off date, no holes)
- [ ] Spatial resolution vs accuracy vs precision (phone GPS ±5–15 m under canopy vs a 10 m Sentinel-2 pixel)

---



## Weekly routine

```
Mon–Thu (~1.5 h/day): learn from the ⭐ resource → reproduce it in your own repo
Sat (~3 h):           build the "Prove it" project
Sun (15 min):         write notes/NN-phase.md → what I learned, one question, one limitation
```

**Before moving to the next phase, ask yourself:**

1. Can I rebuild this phase's project from a blank folder without the tutorial?
2. Does it have tests, a README and a clear statement of its CRS and data assumptions?
3. Could I explain it to a non-technical colleague at Afarinick?

---



## Progress log


| Phase                    | Started | Finished | Repo / artifact link | Notes |
| ------------------------ | ------- | -------- | -------------------- | ----- |
| 0 Setup                  |         |          |                      |       |
| 1 Foundations            |         |          |                      |       |
| 2 Python                 |         |          |                      |       |
| 3 PostGIS                |         |          |                      |       |
| 4 Remote sensing         |         |          |                      |       |
| 5 Field data             |         |          |                      |       |
| 6 Backends and standards |         |          |                      |       |
| 7 Web mapping            |         |          |                      |       |
| 8 Production             |         |          |                      |       |
| 9 Capstone               |         |          |                      |       |


---

*Detailed week-by-week plans for each phase are in* `phase-N/PLAN.md`*. This roadmap supersedes the earlier generic 12-week plan. You've already covered most of that plan's weeks 5–10 through Asase GIS, so this version starts from that level and goes further.*