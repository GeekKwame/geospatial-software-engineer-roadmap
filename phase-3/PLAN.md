# Phase 3 plan: Advanced PostGIS

**Goal:** Move from "PostGIS stores my polygons" to "I can design, query, index and tune a spatial database of a million farm plots".

**Main resource (⭐):** [Official PostGIS workshop](https://postgis.net/workshops/postgis-intro/). Do every module, including Validity, Indexing, Geography, Nearest-Neighbour and Tracking Edit History.

**Database:** use the PostGIS container from `phase-0/docker-compose.yml`:

```bash
cd phase-0
docker compose up -d
docker compose exec postgis psql -U geo -d gis
```

## Part 1: Core PostGIS

- [ ] PostGIS workshop: loading data, geometries, spatial relationships, spatial joins
- [ ] Load your Phase 1 Ghana data with `ogr2ogr`:

  ```bash
  ogr2ogr -f PostgreSQL PG:"host=localhost user=geo dbname=gis password=..." \
    phase-1/data/<districts-file> -nln districts -t_srs EPSG:4326
  ```

- [ ] `geometry` vs `geography`, and when to use each (you saw this with Accra–Kumasi: 1.8 degrees vs 199 km)
- [ ] Typed columns: `geometry(MultiPolygon, 4326)`, and SRIDs
- [ ] Validity: `ST_IsValid`, `ST_IsValidReason`, `ST_MakeValid`, `ST_SnapToGrid`, `ST_ReducePrecision`

## Part 2: Indexes and performance

- [ ] **GiST indexes:** `CREATE INDEX ... USING GIST (geom);`
- [ ] Read query plans with `EXPLAIN ANALYZE`
- [ ] The `&&` bounding-box operator
- [ ] Why `ST_DWithin(a, b, d)` is fast and `ST_Distance(a, b) < d` is slow (the first can use the index)
- [ ] Nearest-neighbour queries with `ORDER BY geom <-> point LIMIT 5`
- [ ] `ST_Subdivide` to split big polygons such as forest reserves, so joins against them are faster
- [ ] Overlap detection: self-join plots on `ST_Intersects`, then measure `ST_Area(ST_Intersection(...)::geography)`
- [ ] Optional: pgRouting, PostGIS raster, topology

## Part 3: Add to Asase GIS (Prove it)

- [ ] A `ForestReserve` / `ProtectedArea` model (synthetic shapes, or open protected-area data if the licence allows)
- [ ] Endpoint `/api/plots/{id}/conflicts/`: overlapping plots and reserve intersections, with overlap area in hectares
- [ ] Endpoint `/api/plots/nearby/?lat=&lon=&radius_m=` using `ST_DWithin` on geography
- [ ] Seed **100,000 synthetic plots** (a management command using `generate_series` or Python)
- [ ] Record `EXPLAIN ANALYZE` timings before and after the GiST index and `ST_Subdivide`, and put them in the README
- [ ] An audit trail for boundary edits: a trigger or `django-simple-history` (who moved a boundary, and when)
- [ ] `docs/queries.sql`: your 15 best spatial queries, each with a comment explaining it
- [ ] Map each SQL concept to its GeoDjango ORM equivalent ([GeoDjango database API](https://docs.djangoproject.com/en/stable/ref/contrib/gis/db-api/))

## Notes

- Write `notes/03-postgis.md`: what you learned, one question, one limitation

## Done when

- [ ] You can explain how a GiST index works (an R-tree over bounding boxes) and why `ST_DWithin` uses it
- [ ] You can give three correct ways to get hectares from EPSG:4326 data
- [ ] The README shows real before-and-after query timings
