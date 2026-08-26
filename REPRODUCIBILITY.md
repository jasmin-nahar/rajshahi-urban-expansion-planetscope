# Reproducibility Notes

## 8-band predictor definitions

```text
NDVI = (NIR - Red) / (NIR + Red)
NDWI = (Green - NIR) / (Green + NIR)
GNDVI = (NIR - Green) / (NIR + Green)
Brightness = (Blue + Green + Red + NIR) / 4
```

## Main LULC RF

The repository uses the updated workflow, not the preliminary RF suite. Candidate feature sets are compared with 5-fold polygon-grouped CV; each CV model uses 120 trees. The one-standard-error rule favors the simplest candidate within one standard error of the highest mean macro-F1. The final selected model uses 700 trees and random seed 42.

## Context correction

Auxiliary binary water model: 500 trees. Published correction parameters in the notebooks: water-probability threshold 30%, small Built/Bare island <=25 pixels with >=75% Waterbody neighbours, tiny Bare/Open hole <=9 pixels with >=80% Built-up neighbours. Vegetation and large open-land patches are not broadly reassigned.

## Final accuracy

Initial design: 40 map-stratified points per mapped class/year, >=50 m from previous training/development-validation samples and >=30 m among final-test points. Final maps are frozen before manual reference interpretation.

## Urban change

Built-up = class 1; other three classes are Non-built-up for binary change. Common river/sandbar exclusion is applied only to urban-growth analysis. New Built-up patches smaller than 9 connected 3 m pixels (81 m²) are removed. Growth-type neighbourhood is 30 m. Primary Gi* grid is 500 m. Road zones are 0–100, >100–250, >250–500 and >500 m.

## Metadata still to complete before DOI/archive release

1. exact PlanetScope acquisition dates and product/scene IDs;
2. exact source/procedure for the common river/sandbar mask;
3. exact OSM extraction/download date and source;
4. exact `pip freeze` from the original final environment, if still available;
5. original 8-band feature-stack-generation code, if available.


## Sentinel-2 robustness workflow

The cross-sensor extension uses the same eight spectral predictors as the main PlanetScope comparison space:

```text
Blue, Green, Red, NIR, NDVI, NDWI, GNDVI, Brightness
```

SWIR-derived predictors are intentionally excluded so the comparison does not gain additional Sentinel-2-only spectral information.

Sentinel-2 sample adaptation rules:

- preserve previously interpreted class labels;
- retain original training polygons only if at least one valid native 10 m pixel center falls inside;
- 10 additional 30 × 30 m training polygons per class/year;
- each augmented polygon is exactly 3 × 3 Sentinel-2 pixels;
- selected augmentation references must have all 9 valid pixels;
- minimum distance from a different-class original training polygon: 10 m;
- minimum spacing among augmented centers: 40 m;
- augmentation source points are excluded from the validation holdout;
- final holdout: 40 points per class/year;
- minimum validation-to-final-training distance: 50 m;
- minimum spacing among validation points: 30 m;
- samples marked `CHECK_RGB` require visual verification against source imagery.

The exact `OrigRef_ID` selections used by the reported analysis are explicitly archived in notebook 12 to make the sampling decision reproducible.

Sentinel-2 RF settings:

- grouped CV folds: 5
- CV trees: 120
- final trees: 700
- `max_features="sqrt"`
- `max_depth=None`
- `min_samples_leaf=1`
- `class_weight="balanced_subsample"`
- bootstrap: True
- random seed: 42
- maximum training pixels per polygon: 100

## Cross-sensor common-domain harmonization

Notebook 14:

1. reads the exact final frozen/context-corrected PlanetScope class maps and the final Sentinel-2 class maps;
2. intersects all four raster footprints;
3. builds one 10 m EPSG:32645 comparison grid;
4. aggregates PlanetScope 3 m categories to 10 m with categorical `mode`;
5. aligns Sentinel-2 with nearest-neighbour resampling;
6. keeps only cells valid in all four maps;
7. removes the common river/sandbar exclusion (`non-zero = excluded`);
8. computes class areas and built-up change on exactly the same cells;
9. reports four-class pixel agreement, Built-up IoU/Jaccard and Dice agreement; and
10. writes the exact input paths and harmonization settings to `Cross_Sensor_Input_Provenance.json`.

The resulting 10 m PlanetScope values are **comparison-only** and do not replace the native 3 m PlanetScope manuscript results.
