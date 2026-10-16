# Phase 1 plan: GIS and geodesy foundations

**Goal:** Think like a GIS analyst. Most GIS bugs in software come from misunderstood basics: the wrong coordinate system, swapped latitude and longitude, invalid geometry, or area measured in degrees.

**Main resource (⭐):** [Spatial Thoughts: Introduction to QGIS](https://courses.spatialthoughts.com/introduction-to-qgis.html)

## Folder layout

```text
phase-1/
├── data/                   ← downloaded datasets (not pushed to git)
│   └── qgis-course/        ← Spatial Thoughts course data package
├── exports/                ← PDF maps
└── ghana-cocoa-belt.qgz    ← your QGIS project (save it here)
```

## Part 1: QGIS basics and data

- [ ] Work through the first modules of the Spatial Thoughts QGIS course
- [ ] Download into `phase-1/data/`:
  - [ ] [Ghana administrative boundaries from HDX](https://data.humdata.org/dataset/cod-ab-gha) (regions and districts)
  - [ ] [Geofabrik Ghana extract](https://download.geofabrik.de/africa/ghana.html) (take the `.shp.zip`; it has roads and places)
- [ ] Load both into QGIS and practise:
  - [ ] Styling layers (colours, labels, categorised styles)
  - [ ] Opening attribute tables and filtering features
  - [ ] Selecting features by attribute and by location
- [ ] Learn the difference between vector data (points, lines, polygons) and raster data (grids of pixels)

## Part 2: Coordinate systems and geometry

- [ ] Learn the difference between a **datum**, a **projection** and a **CRS** (coordinate reference system), and what an EPSG code is
  - Optional maths: [Snyder, *Map Projections: A Working Manual*](https://pubs.usgs.gov/publication/pp1395), chapters 1–8
- [ ] Learn when to use each of Ghana's systems:
  - [EPSG:4326 (WGS 84)](https://epsg.io/4326): GPS and GeoJSON
  - [EPSG:32630 (UTM 30N)](https://epsg.io/32630): metric work (areas, distances) in most of Ghana
  - [EPSG:2136](https://epsg.io/2136) and [EPSG:25000](https://epsg.io/25000): legacy systems on older survey and forest-reserve maps
- [ ] Understand why area and distance need a projected CRS or geodesic maths. Eastern Ghana falls in UTM 31N, so know when that matters.
- [ ] Practise the core tools: buffer, clip, intersect, dissolve, spatial join
- [ ] Learn what makes a geometry invalid: self-intersections ("figure-eights"), unclosed rings, overlaps, gaps, slivers
- [ ] Learn the file formats: GeoJSON (longitude before latitude), Shapefile and its limits, GeoPackage (the modern default), KML, GeoTIFF

## Part 3: Build the "Ghana Cocoa Belt" project (Prove it)

- [ ] Add regions, districts, OSM roads and settlements
- [ ] Add forest-loss data from [Global Forest Watch](https://www.globalforestwatch.org/) for the Western, Ashanti or Eastern region
- [ ] Draw about 20 made-up farm polygons (synthetic, never real farmer data)
- [ ] Reproject everything to UTM 30N (EPSG:32630) and calculate each farm's area in hectares (`$area / 10000` in the field calculator)
- [ ] Break 3 polygons on purpose, then fix them with *Check Validity* and *Fix Geometries*
- [ ] Make a print layout (map, legend, scale bar, north arrow, title) and export it to `phase-1/exports/`
- [ ] Write `notes/01-crs-cheatsheet.md`: which CRS to use for what in Ghana, and why

## Throughout the phase

- Add every new term to `notes/00-glossary.md` (datum, EPSG, CRS, dissolve, ...)
- **At work:** ask your manager or IT lead which GIS tools, formats and coordinate systems Afarinick uses

## Done when

- [ ] You can explain datum vs projection vs CRS out loud in 2 minutes
- [ ] The QGIS project, the PDF map and the CRS cheat sheet all exist
- [ ] You can explain why measuring area in EPSG:4326 gives a meaningless number
