# Phase 1 plan: GIS and geodesy foundations

**Goal:** Think like a GIS analyst. Most GIS bugs in software come from misunderstood basics: the wrong coordinate system, swapped latitude and longitude, invalid geometry, or area measured in degrees.

**Main resource (⭐):** [Spatial Thoughts: Introduction to QGIS](https://courses.spatialthoughts.com/introduction-to-qgis.html)

**Companion lab:** [Ernest Opoku-Kwarteng's Geospatial Developers Module 1](https://github.com/ernest19/Geospatial_Developers/tree/main/module_1). It is a practical, Ghana-focused introduction to loading layers, layer order, cartography, basemaps, georeferencing and qgis2web. Use it for extra practice, not as a second course to finish.

**Prove-it project:** a reproducible **Ghana Cocoa Belt** QGIS project, a print map and a short CRS decision guide.

## Folder layout

```text
phase-1/
├── PLAN.md
├── course/                 ← exercises and temporary QGIS projects
├── data/                   ← downloaded datasets (not pushed to git)
│   ├── raw/                ← unchanged source downloads
│   └── processed/          ← cleaned/reprojected working layers
├── exports/                ← final PDF/PNG map and optional web preview
└── ghana-cocoa-belt.qgz   ← final QGIS project
```

Keep source data unchanged in `data/raw/`. Export derived layers to `data/processed/`, preferably in one GeoPackage. Use relative paths and reopen the project once before calling it finished.

## Part 1: Become comfortable in QGIS

- [ ] Work through the first modules of the Spatial Thoughts QGIS course
- [ ] Learn the QGIS mental model:
  - [ ] **Project** (`.qgz`) vs **layer** vs **data source**; saving a project does not copy its data
  - [ ] Browser, Layers, Layer Styling and Processing Toolbox panels
  - [ ] Pan, zoom, zoom to layer/selection, identify features and measure
  - [ ] Project CRS vs layer CRS, and what on-the-fly reprojection does
- [ ] Load one point, one line, one polygon and one raster layer
- [ ] Reorder the layers deliberately: basemap/raster at the bottom, polygons next, then lines and points
- [ ] Inspect every layer before analysis:
  - [ ] geometry type, feature count, extent, CRS and units
  - [ ] attribute names, data types, missing values and a unique identifier
  - [ ] source organisation, publication date, licence and known limitations
- [ ] Filter and select features by attribute and by location; save only the selected features to a new layer
- [ ] Make one attribute join (for example, a population CSV to districts) and explain why stable IDs are safer than joining on names

### Practice data

- [ ] Download into `phase-1/data/raw/`:
  - [ ] [Ghana administrative boundaries from HDX](https://data.humdata.org/dataset/cod-ab-gha) (regions and districts)
  - [ ] [Geofabrik Ghana extract](https://download.geofabrik.de/africa/ghana.html) (roads and settlements)
- [ ] Optional: use the Ghana districts, regions, health facilities, railways and population files in [Ernest's course dataset](https://github.com/ernest19/Geospatial_Developers/tree/main/datasets) for the interface exercises
- [ ] Create `phase-1/SOURCES.md` with, for each final-project dataset: source URL, download date, licence, original CRS and what you use it for

> Training datasets can become stale. Ernest's dataset is convenient for exercises; use a current, authoritative or well-maintained source for the final map and verify its licence before republishing it.

## Part 2: Understand data models and formats

- [ ] Explain vector points/lines/polygons vs raster cells, and choose the right model for farms, roads, settlements, elevation and satellite imagery
- [ ] Compare these formats by opening or exporting the same layer:
  - [ ] **Shapefile:** a multi-file legacy format with field-name, type and encoding limitations
  - [ ] **GeoPackage:** the preferred working format; multiple vector/raster layers and tables in one SQLite file
  - [ ] **GeoJSON:** good for web interchange; WGS 84 and longitude before latitude under RFC 7946
  - [ ] **KML:** common field/GPS interchange, but not a strong analysis format
  - [ ] **GeoTIFF:** georeferenced raster data
- [ ] Package the final vector layers into `data/processed/ghana-cocoa-belt.gpkg` with clear lowercase names
- [ ] Learn the difference between a **temporary/scratch layer** and a saved layer so work is not lost when QGIS closes

## Part 3: Coordinate systems and measurement

- [ ] Learn the difference between a **datum**, a **projection** and a **CRS** (coordinate reference system), and what an EPSG code is
  - Optional maths: [Snyder, *Map Projections: A Working Manual*](https://pubs.usgs.gov/publication/pp1395), chapters 1–8
- [ ] Learn when to use each of Ghana's systems:
  - [ ] [EPSG:4326 (WGS 84)](https://epsg.io/4326): GPS and GeoJSON
  - [ ] [EPSG:32630 (WGS 84 / UTM zone 30N)](https://epsg.io/32630): metric work in most of Ghana
  - [ ] [EPSG:32631 (WGS 84 / UTM zone 31N)](https://epsg.io/32631): metric work in far-eastern Ghana
  - [ ] [EPSG:2136](https://epsg.io/2136) and [EPSG:25000](https://epsg.io/25000): legacy systems on older survey and forest-reserve maps
- [ ] Distinguish **assign/set CRS** (metadata) from **reproject/transform** (new coordinates). Never use "set CRS" to force a misplaced layer to line up.
- [ ] Make a controlled measurement experiment:
  - [ ] measure the same farm in EPSG:4326, UTM 30N and UTM 31N
  - [ ] record the area and units in `notes/01-crs-cheatsheet.md`
  - [ ] explain which result you trust and how distance from the UTM zone affects the choice
- [ ] Put one known Accra or Kumasi coordinate into QGIS twice—once correctly and once with latitude/longitude swapped—and diagnose the bad point from its extent
- [ ] Inspect a legacy Ghana layer's CRS and datum transformation before combining it with WGS 84 data

## Part 4: Spatial analysis and data quality

- [ ] Practise the core tools: buffer, clip, intersect, dissolve and spatial join
- [ ] For every tool, predict the output geometry and attributes before running it, then check feature counts and spot-check the result
- [ ] Learn the main spatial predicates: intersects, within, contains, touches and overlaps
- [ ] Learn what makes a geometry invalid: self-intersections ("figure-eights"), unclosed rings, duplicate vertices and collapsed parts
- [ ] Distinguish **invalid geometry** from valid-but-bad data such as slivers, gaps, overlaps and duplicate features
- [ ] Enable snapping and topological editing, then digitise adjacent polygons without accidental gaps or overlaps
- [ ] Deliberately create and document at least three failures:
  - [ ] a self-intersecting polygon
  - [ ] overlapping farm polygons or a narrow sliver
  - [ ] a layer with the wrong assigned CRS or swapped coordinates
- [ ] Diagnose each failure first, then repair it with *Check Validity*, *Fix Geometries*, snapping or the correct CRS operation; note whether the repair changed the geometry
- [ ] Save a Processing Model or processing history for one multi-step workflow (for example: reproject → fix geometries → clip → calculate area)

## Part 5: Cartography and communication

- [ ] Style regions or districts with an appropriate categorised or graduated renderer; explain why the classification and colour scheme fit the data
- [ ] Label without making the map unreadable; set scale-dependent visibility where useful
- [ ] Add an OSM basemap through QGIS XYZ Tiles or QuickMapServices and note:
  - [ ] the basemap is normally served in EPSG:3857, but that does not make it suitable for measuring area
  - [ ] tiles are an external service, not part of the saved project
  - [ ] the provider's licence, attribution and usage policy still apply
- [ ] Create a print layout with title, legend, scale bar, north arrow, data sources, author, date and CRS
- [ ] Check the layout at its exported size, not only while zoomed in inside QGIS

## Part 6: Build the "Ghana Cocoa Belt" project (Prove it)

- [ ] Pick one study area in Ghana's cocoa belt and write a one-sentence map question
- [ ] Add regions, districts, OSM roads and settlements
- [ ] Add forest-loss data from [Global Forest Watch](https://www.globalforestwatch.org/) for the study area; treat it as an introduction to raster/thematic data, not a deforestation verdict (that comes in Phase 4)
- [ ] Draw about 20 made-up farm polygons (synthetic, never real farmer data) with `plot_id`, `crop`, `survey_date`, `area_ha` and `source` fields
- [ ] Reproject the analysis layers to the appropriate UTM zone and calculate each farm's area in hectares (`$area / 10000` in the field calculator)
- [ ] Run validity and overlap checks and resolve or document every warning
- [ ] Use a spatial join to attach the containing district to each synthetic farm
- [ ] Export a print layout to `phase-1/exports/ghana-cocoa-belt.pdf` and a PNG preview
- [ ] Write `notes/01-crs-cheatsheet.md`: which CRS to use for storage, web exchange, display and measurement in Ghana, and why
- [ ] Write a short `phase-1/README.md` with the map question, workflow, data sources, CRS decisions, limitations and a screenshot

### Optional stretch exercises from Ernest's course

Choose at most one now; neither is required to finish Phase 1.

- [ ] **Georeferencing:** georeference a public scanned map with ground control points, inspect residual errors and export a GeoTIFF. Do not treat a visually aligned result as survey-grade data.
- [ ] **Web preview:** export a small, non-sensitive layer with qgis2web and inspect the generated Leaflet/OpenLayers files. Treat this as a preview; Phase 7 covers production web mapping.

## Throughout the phase

- Add every new term to `notes/00-glossary.md` (datum, EPSG, CRS, dissolve, predicate, GCP, ...)
- After each session, add three lines to `notes/01-learning-log.md`: **learned**, **confused by**, **next experiment**
- **At work:** ask your manager or IT lead which GIS tools, formats, coordinate systems and data-quality checks Afarinick uses
- Keep real farmer identities and boundaries out of this public repository

## Done when

- [ ] You can explain project vs layer vs data source, and datum vs projection vs CRS, out loud in 2 minutes each
- [ ] You can inspect an unfamiliar layer and identify its geometry, CRS, extent, attributes, provenance and likely problems
- [ ] You can explain why measuring area in EPSG:4326 is wrong and choose an appropriate measurement method for a Ghanaian plot
- [ ] You can diagnose a missing/misplaced layer, invalid polygon and bad join without blindly clicking repair tools
- [ ] The `.qgz` reopens without broken layers on a clean path
- [ ] The QGIS project, GeoPackage, PDF/PNG map, `phase-1/SOURCES.md`, project README and CRS cheat sheet all exist
