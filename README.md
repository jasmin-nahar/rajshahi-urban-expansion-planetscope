# Rajshahi Urban Expansion — PlanetScope 2018–2026

Reproducible analysis code for the manuscript **Fine-Resolution Assessment of Land Use/Land Cover Change, Urban Expansion Types, Growth Hotspots and Road Proximity in Rajshahi City Using PlanetScope Imagery (2018–2026)**.

## What is included

The repository reproduces the final reported workflow: updated year-specific Random Forest classification, conservative context correction, independent final LULC accuracy, river/sandbar-excluded built-up change, MMU filtering, Infill–Edge–Leapfrog classification, 500 m Getis-Ord Gi* hotspots, current-OSM road proximity, and final summary outputs.

## Important data note

Raw PlanetScope imagery is not distributed. The uploaded notebook archive also did not contain the original notebook that generated the two 8-band spectral/index feature stacks. Therefore the public workflow begins from:

- `Outputs/Spectral_Indices/2018/FeatureStack_2018_8bands.tif`
- `Outputs/Spectral_Indices/2026/FeatureStack_2026_8bands.tif`

Expected band order: `Blue, Green, Red, NIR, NDVI, NDWI, GNDVI, Brightness`.

## Final main-classifier settings

- 5-fold `StratifiedGroupKFold` feature-set comparison
- 120 trees per grouped-CV candidate model
- one-standard-error feature-set selection
- **700 trees** in the final LULC classifier
- `max_features="sqrt"`
- `max_depth=None`
- `min_samples_leaf=1`
- `class_weight="balanced_subsample"`
- bootstrap sampling
- random seed 42
- at most 100 randomly sampled training pixels per polygon

The context-correction workflow uses a separate **500-tree auxiliary binary water model**; it is not the main LULC RF.

## Run order

```text
00_Texture_Stack_and_Sample_QC.ipynb
01_RF_Classification_2018.ipynb
02_RF_Classification_2026.ipynb
03_Context_Correction_2018.ipynb
04_Context_Correction_2026.ipynb
05_Create_Final_Test_Points.ipynb
[MANUALLY LABEL Ref_ID FROM DATE-MATCHED SOURCE IMAGERY]
06_Final_Independent_Accuracy_Assessment.ipynb
07_BuiltUp_Change_NoRiver_MMU9.ipynb
08_Urban_Growth_Type_Infill_Edge_Leapfrog.ipynb
09_Urban_Growth_Hotspot_GiStar_500m.ipynb
10_Road_Proximity_Analysis_Current_OSM.ipynb
11_Final_Results_Summary.ipynb
```

## Environment

Original analysis environment: Python 3.11.9.

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Set `RAJSHAHI_PROJECT_ROOT` to the local analysis root when using the original folder structure. If it is not set, notebooks attempt to use the repository root.

See `DATA_REQUIREMENTS.md`, `REPRODUCIBILITY.md`, and `GITHUB_UPLOAD_STEPS.md` before public release.
