# Phase 1 data sources

Record a dataset **when you download it**, before you start changing it. One row per source dataset is enough; add detail below the table when a caveat affects the map.

| Dataset | Publisher | Source URL | Downloaded | Version/date | Licence | Original CRS | Local raw file | Used for | Limitations |
| ------- | --------- | ---------- | ---------- | ------------ | ------- | ------------ | -------------- | -------- | ----------- |
| Example: Ghana administrative boundaries | Add publisher | Add direct dataset page | YYYY-MM-DD | Add release date | Add licence | Verify in QGIS | `data/raw/...` | Region/district context | Add boundary vintage and known gaps |
| Ghana administrative boundaries | | | | | | | | | |
| Ghana roads and settlements | | | | | | | | | |
| Forest-loss layer | | | | | | | | | |

## Checks before use

- [ ] I opened the publisher's dataset page, rather than relying only on a copied download.
- [ ] I verified the licence permits the way I will publish the result.
- [ ] I recorded the dataset's date or version; "latest" is not a reproducible version.
- [ ] I checked geometry type, feature count, extent, CRS and units in QGIS.
- [ ] I checked important fields, missing values and whether the supposed ID is unique.
- [ ] I kept the original download unchanged under `data/raw/`.
- [ ] I recorded every material cleaning, repair, join or reprojection below.

## Processing log

| Date | Input | Operation | Output | Reason/check |
| ---- | ----- | --------- | ------ | ------------ |
| YYYY-MM-DD | `data/raw/...` | Example: fix geometries, reproject, clip | `data/processed/ghana-cocoa-belt.gpkg` | State what was checked after the operation |

## Decisions and caveats

Add short notes here when a decision cannot be captured in the tables. Examples: why a particular boundary source was selected, whether a datum transformation was applied, or why two sources do not align perfectly.
