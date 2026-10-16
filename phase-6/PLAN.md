# Phase 6 plan: Geospatial backends and standards (Weeks 16–18)

**Goal:** Serve spatial data the way professional systems do: fast vector tiles, standard OGC APIs, and dynamic raster tiles.

**Main resource (⭐):** [pygeoapi workshop, "Diving into pygeoapi"](https://dive.pygeoapi.io/)

## Week 16: GeoDjango and DRF-GIS in depth

- [ ] GeoDjango: `GEOSGeometry`, spatial lookups (`intersects`, `dwithin`, `contains`), `Transform`, `Area`, GIS admin widgets
- [ ] Write custom `Func` wrappers for `ST_*` functions GeoDjango doesn't expose
- [ ] `djangorestframework-gis`: `GeoFeatureModelSerializer`, bounding-box filters (`InBBoxFilter`), paginated FeatureCollections
- [ ] Try the FastAPI + GeoAlchemy2 alternative for one small endpoint
- [ ] Watch: [Maps with GeoDjango, PostGIS and Leaflet](https://djangotv.com/videos/djangocon-europe/2019/djangocon-2019-maps-with-geodjango-postgis-and-leaflet/)

## Week 17: OGC standards and vector tiles

- [ ] **OGC standards:** what WMS and WFS are (legacy but everywhere), and **OGC API – Features** (the modern REST version)
- [ ] Work through the pygeoapi workshop
- [ ] **Vector tiles (MVT):**
  - [ ] The `/z/x/y` tile scheme and how tile coordinates map to the world
  - [ ] `ST_AsMVT` and `ST_AsMVTGeom` in PostGIS
  - [ ] Tile servers: [Martin](https://maplibre.org/martin/) and [pg_tileserv](https://github.com/CrunchyData/pg_tileserv)
  - [ ] Static tiles: [PMTiles](https://docs.protomaps.com/) and [tippecanoe](https://github.com/felt/tippecanoe)
- [ ] Watch: [How to visualise millions of features](https://www.youtube.com/watch?v=ifkl30N-_-w)
- [ ] GeoServer basics ([getting started](https://docs.geoserver.org/latest/en/user/gettingstarted/index.html)), because many government and NGO partners use it

## Week 18: Add to Asase GIS (Prove it)

- [ ] Martin (or a Django `ST_AsMVT` view) serving your 100k plots as vector tiles
- [ ] An OGC API – Features endpoint via pygeoapi, pointing at the same PostGIS database
- [ ] [TiTiler](https://developmentseed.org/titiler/) serving your NDVI COGs from Phase 4
- [ ] Add all of these to `docker-compose.yml`
- [ ] README: document each service, with an architecture diagram

## Notes

- Write `notes/06-backends.md`: what you learned, one question, one limitation

## Done when

- [ ] `docker compose up` starts PostGIS, Django, Martin, pygeoapi and TiTiler
- [ ] You can explain when to use vector tiles vs GeoJSON vs WMS
- [ ] 100k plots load smoothly as tiles in a test map
