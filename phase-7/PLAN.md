# Phase 7 plan: Modern web mapping

**Goal:** Build map interfaces that field officers and managers actually want to use, and that can display 100k+ plots smoothly.

**Main resource (⭐):** [MapLibre GL JS examples](https://maplibre.org/maplibre-gl-js/docs/examples/) (work through 20+) and the [MapLibre style spec](https://maplibre.org/maplibre-style-spec/)

## Part 1: MapLibre, drawing and Turf

- [ ] **MapLibre GL JS:**
  - [ ] Sources and layers, and how a style is put together
  - [ ] Data-driven styling (colour plots by a property)
  - [ ] `feature-state` for hover and selection
  - [ ] Vector tile sources pointing at your Martin server from Phase 6
- [ ] **Drawing and editing polygons:** [Terra Draw](https://terradraw.io/) with MapLibre (or [Leaflet-Geoman](https://geoman.io/docs/leaflet) in Leaflet), with snapping
- [ ] **[Turf.js](https://turfjs.org/):** `area`, `intersect` and `kinks` (self-intersection) for instant feedback in the browser
- [ ] Skim the [OpenLayers workshop](https://openlayers.org/workshop/en/); it's common in government and enterprise systems
- [ ] Look at [deck.gl](https://deck.gl/) and [kepler.gl](https://kepler.gl/) for big-data visualisation
- [ ] Map UX: clustering, legends, filters, mobile layouts, and slow 3G connections in rural Ghana

## Part 2: React + MapLibre frontend for Asase GIS (Prove it)

- [ ] A vector-tile layer of all plots, coloured by EUDR risk from Phase 4
- [ ] Click a plot → side panel with its attributes, NDVI chart and conflicts
- [ ] Draw or edit a plot → live area and overlap warnings with Turf → save via the API
- [ ] Server-side validation with `plotcheck` on save (never trust the browser alone)
- [ ] Filters by district, crop, risk and planting year
- [ ] Works on a phone; test it with the browser's mobile view and network throttling

## Notes

- Write `notes/07-web-mapping.md`: what you learned, one question, one limitation

## Done when

- [ ] 100k plots pan and zoom smoothly
- [ ] A field officer could draw a plot on a phone and get clear error messages
- [ ] You know which libraries use latitude/longitude order (Leaflet's `LatLng`) and which use longitude/latitude (MapLibre, GeoJSON, Turf)
