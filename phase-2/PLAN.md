# Phase 2 plan: Geospatial Python (Weeks 4–6)

**Goal:** Do everything you did in QGIS, but in reproducible, testable Python.

**Main resource (⭐):** [Spatial Thoughts: Python Foundation for Spatial Analysis](https://courses.spatialthoughts.com/python-foundation.html)
**Backup:** [Automating GIS Processes (University of Helsinki)](https://autogis-site.readthedocs.io/en/latest/)

**Prove-it project:** `plotcheck`, an EUDR plot-validator command-line tool and Python package, in its own GitHub repo.

## Week 4: GeoPandas and the GDAL command line

- [ ] Work through the Spatial Thoughts Python course
- [ ] Redo your Phase 1 QGIS work in a Jupyter notebook, using the same Ghana data:
  - [ ] `gpd.read_file(..., engine="pyogrio")` to load regions, districts and roads
  - [ ] `to_crs(32630)` and `.area / 10_000` to get hectares
  - [ ] `sjoin` (which district is each farm in?), `overlay`, `dissolve`, `clip`, `.buffer`
- [ ] Learn the GDAL command line:
  - [ ] `ogrinfo` to inspect a file
  - [ ] `ogr2ogr` to convert formats (Shapefile → GeoPackage → GeoJSON), reproject (`-t_srs EPSG:32630`) and filter (`-where`, `-sql`)
  - [ ] `gdalinfo` on a raster

## Week 5: Shapely 2, pyproj and messy data

- [ ] **Shapely 2:**
  - [ ] Validity: `is_valid`, `is_valid_reason`, `make_valid`, `set_precision`
  - [ ] Predicates: `intersects`, `within`, `covers`
  - [ ] `STRtree` spatial index for fast "which plots overlap?" checks
- [ ] **pyproj:**
  - [ ] `Transformer.from_crs(..., always_xy=True)`, and why the latitude/longitude order is a trap
  - [ ] Geodesic area with `Geod(ellps="WGS84").geometry_area_perimeter(...)`
- [ ] Practise on messy inputs: KML exported from a phone, a CSV of GPS points, mixed CRS, duplicate vertices, 3D (Z) coordinates

## Week 6: Build `plotcheck` (Prove it)

Create a new repo (for example `plotcheck`) with a package layout, a CLI (`typer` or `click`), and pytest tests.

- [ ] **Read** GeoJSON, KML, GeoPackage and CSV
- [ ] **Normalise** to EPSG:4326, longitude first, rounded to 6 decimal places
- [ ] **Flag or fix:** unclosed rings, self-intersections, holes (split them, following EUDR guidance), duplicate vertices, slivers, suspiciously tiny or huge plots
- [ ] **Area** in hectares, both UTM 30N and geodesic, and report the difference
- [ ] **Rule:** plots over 4 ha must be polygons, not points
- [ ] **Overlaps** between plots, using `STRtree`
- [ ] **Output** a cleaned EUDR-style GeoJSON plus a CSV or HTML error report
- [ ] **Tests:** hand-crafted bad geometries (figure-eight, unclosed ring, hole, duplicate points, swapped lat/lon)
- [ ] **CI:** GitHub Actions running the tests on every push
- [ ] **README:** what it checks, how to install and run it, and its CRS assumptions

Read the [EUDR GeoJSON file rules](https://eudr.webcloud.ec.europa.eu/tracesnt/help/eudr-documentation/operator/geojson-description.html) before you start; they are the spec you're implementing.

## Notes

- Write `notes/02-python.md`: what you learned, one question, one limitation

## Done when

- [ ] `plotcheck` is on GitHub with tests passing in CI
- [ ] You can explain `always_xy=True` and why GeoJSON is longitude-first
- [ ] You can explain how `make_valid` can silently change what a polygon means
