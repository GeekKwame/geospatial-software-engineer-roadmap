# Phase 8 plan: Production, scale and cloud-native

**Goal:** Use your DevOps and AWS strengths in a geospatial setting. This is where you can pull ahead of most GIS developers.

**Main resource (⭐):** [Cloud-Native Geospatial Guide](https://guide.cloudnativegeo.org/)

## Part 1: Containers, background jobs and testing

- [ ] Docker images with GDAL that actually work:
  - Start from the [official GDAL images](https://github.com/OSGeo/gdal/tree/master/docker)
  - Pin the versions of GDAL, PROJ and GEOS
- [ ] **Background jobs** with Celery (or RQ) for heavy work: Kobo imports, satellite checks, report generation
- [ ] **Testing geospatial code:**
  - [ ] Geometry fixtures (valid, invalid, edge cases)
  - [ ] Property-based tests with Hypothesis (for example: area is never negative, reprojecting there and back changes nothing beyond tolerance)
  - [ ] Snapshot tests of GeoJSON output
  - [ ] Tests across CRS
  - [ ] [pytest-django](https://pytest-django.readthedocs.io/) against a real PostGIS database
- [ ] Safe migrations that alter geometry columns; PostGIS backup and restore

## Part 2: Cloud-native data and analytics

- [ ] **COGs on S3** + CloudFront for rasters ([cogeo.org](https://cogeo.org/))
- [ ] **PMTiles on S3** for vector tiles without a tile server
- [ ] **[GeoParquet](https://geoparquet.org/)** for exports and analytics
- [ ] **[DuckDB spatial](https://duckdb.org/docs/stable/core_extensions/spatial/overview)**: query GeoParquet files with SQL
- [ ] **[H3](https://h3geo.org/)** hexagons for aggregating plots into regional dashboards
- [ ] Look at [Sentinel-2 COGs on AWS Open Data](https://registry.opendata.aws/sentinel-2-l2a-cogs/)
- [ ] Observability: log slow spatial queries, track tile cache hit rates
- [ ] Licensing and attribution: OSM (ODbL), Copernicus, Hansen (CC-BY); data protection for farmer data

## Part 3: Deploy (Prove it)

- [ ] Deploy Asase GIS to AWS with Terraform:
  - [ ] PostGIS on RDS
  - [ ] COGs and PMTiles on S3 + CloudFront
  - [ ] A Celery worker for satellite checks
- [ ] GitHub Actions: lint → tests against a PostGIS service container → build the image → deploy
- [ ] A nightly export of all plots to **GeoParquet**, plus an EUDR-format **GeoJSON** per cooperative or district
- [ ] An H3-aggregated "risk by district" dashboard view
- [ ] Set an AWS budget alert before you deploy anything

## Notes

- Write `notes/08-production.md`: what you learned, one question, one limitation

## Done when

- [ ] Asase GIS runs on AWS from a single `terraform apply`
- [ ] A push to `main` runs tests and deploys automatically
- [ ] Nightly exports appear in S3
