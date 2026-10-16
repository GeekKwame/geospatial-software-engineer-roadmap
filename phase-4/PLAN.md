# Phase 4 plan: Remote sensing and raster data

**Goal:** Answer the question at the centre of the EUDR: **"Has this plot lost forest since 31 December 2020?"**

**Main resources (⭐):**
- [Spatial Thoughts: End-to-End Google Earth Engine](https://courses.spatialthoughts.com/end-to-end-gee.html)
- [Digital Earth Africa training](https://training.digitalearthafrica.org/) (free, Africa-focused)

**Earth Engine reminder:** your free account is for noncommercial learning only. Don't use it for Afarinick work. If your project shows "not registered", finish registration at [console.cloud.google.com/earth-engine/configuration](https://console.cloud.google.com/earth-engine/configuration).

**Prove-it project:** `forestcheck`, an EUDR deforestation checker.

## Part 1: Raster basics and satellites

- [ ] Raster basics: bands, resolution, nodata, data types, the affine transform, CRS
- [ ] Satellites:
  - Sentinel-2: 10 m pixels, a new image every 5 days, free
  - Landsat: 30 m pixels, archive back to the 1980s
  - Why clouds are a big problem over Ghana's forest zone, and why Sentinel-1 radar (which sees through cloud) helps
- [ ] Explore Ghana in the [Copernicus Browser](https://browser.dataspace.copernicus.eu/) (you have an account)
- [ ] Spectral indices: **NDVI** = (NIR − Red) / (NIR + Red), and NDMI
- [ ] Cloud masking with the Sentinel-2 SCL band

## Part 2: Earth Engine

- [ ] Spatial Thoughts End-to-End GEE course, modules 1–3 ([Module 1 video](https://www.youtube.com/watch?v=daYhxVVIpJU))
- [ ] In the Code Editor: filter Sentinel-2, mask clouds, make a median composite, compute NDVI (your Accra script is a start)
- [ ] Load the forest datasets:
  - [Hansen Global Forest Change](https://developers.google.com/earth-engine/datasets/catalog/UMD_hansen_global_forest_change_2024_v1_12) (tree-cover loss by year)
  - [JRC Global Forest Cover 2020](https://developers.google.com/earth-engine/datasets/catalog/JRC_GFC2020_V2) (the EU's reference map for 31 December 2020)
- [ ] Zonal statistics: `reduceRegions` to summarise pixels inside each farm polygon
- [ ] Python API: `earthengine authenticate`, `ee.Initialize(project=...)`, and `geemap` in Jupyter

## Part 3: Open data in Python (no Google)

- [ ] **COG** (Cloud Optimized GeoTIFF) and **STAC** (catalogues of satellite images)
- [ ] Search Sentinel-2 with `pystac-client` on [Earth Search](https://element84.com/earth-search/) or [Planetary Computer](https://planetarycomputer.microsoft.com/docs/quickstarts/reading-stac/)
- [ ] Load a time series with `odc-stac` or `stackstac` into `xarray`
- [ ] **rasterio:** read, windowed reads, reproject, mask by polygon
- [ ] **rioxarray:** `.rio.clip(...)`, `.rio.reproject(...)`
- [ ] Study [FAO Open Foris Whisp](https://openforis.org/solutions/whisp/): how does it decide deforestation risk?

## Part 4: Build `forestcheck` (Prove it)

As a module in Asase GIS or a standalone repo. For each plot polygon:

- [ ] Was the plot forest on 31 December 2020? (JRC GFC2020)
- [ ] How much tree-cover loss has there been since 2021? (Hansen)
- [ ] A Sentinel-2 NDVI time series from 2020 to now (via STAC or Earth Engine)
- [ ] A **risk flag** (low / medium / high) with a written explanation
- [ ] A PNG or HTML "plot report card"
- [ ] Bonus: for rehabilitation plots, show NDVI recovery after replanting
- [ ] README **Limitations** section: 10–30 m pixels, cloud cover, and the fact that cocoa under shade trees is hard to tell apart from forest

## Notes

- Write `notes/04-remote-sensing.md`: what you learned, one question, one limitation

## Done when

- [ ] You can explain NDVI, and why it can't reliably tell shaded cocoa from forest
- [ ] You can explain how COG + STAC let you read part of a satellite image without downloading all of it
- [ ] `forestcheck` produces a report card for a test plot
