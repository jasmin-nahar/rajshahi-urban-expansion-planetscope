# Sentinel-2 GitHub Update — Upload Guide

Upload/replace these items in the existing repository:

1. `gee/01_GEE_Sentinel2_Seasonal_Export_2018_2026.js`
2. `notebooks/12_Sentinel2_Training_Validation_Preparation.ipynb`
3. `notebooks/13_Sentinel2_RF_Classification_2018_2026.ipynb`
4. `notebooks/14_PlanetScope_vs_Sentinel2_Common_Domain_Comparison.ipynb`
5. `Samples/Sentinel2_RF_Samples_Adapted.gpkg`
6. `Samples/Sentinel2_Sample_Design_Report.txt`
7. replace `README.md`
8. replace `DATA_REQUIREMENTS.md`
9. replace `REPRODUCIBILITY.md`
10. replace `NOTEBOOK_MANIFEST.md`
11. replace `Samples/README.md`
12. replace `.gitignore`

Do not upload raw PlanetScope imagery, raw Sentinel-2 GeoTIFFs, model binaries, or large Outputs folders.

After upload, create a new GitHub release only after the `CHECK_RGB` sample review and the final common-domain rerun are frozen.
