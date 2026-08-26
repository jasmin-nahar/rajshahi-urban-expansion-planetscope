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
