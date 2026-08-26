# Notebook Manifest

## Included final workflow

- updated RF texture/QC and year-specific classifiers;
- 2018 and 2026 context correction;
- final-test point generation and final independent accuracy;
- stable-domain MMU9 built-up change;
- Infill/Edge/Leapfrog classification;
- 500 m Getis-Ord Gi* hotspot analysis;
- fixed no-Fiona current-OSM road analysis;
- final summary, extended only to collect the already-completed road outputs.

## Excluded as superseded / development-only

- the older `Rajshahi_RF_Classification_Notebooks` suite;
- `03_RF_Accuracy_Area_and_Change_2018_2026_Updated.ipynb` (development-stage summary);
- `2018_2026_Context_Final_Change_READY_TO_RUN.ipynb` (superseded by river-excluded MMU9 change notebook);
- bundled development CSV/TIF artifacts from the context-correction folder.


## Google Earth Engine script

`gee/01_GEE_Sentinel2_Seasonal_Export_2018_2026.js` creates the March–April 2018 and 2026 four-band Sentinel-2 SR composites used by notebooks 12–14.
