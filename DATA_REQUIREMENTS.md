# Data Requirements

## PlanetScope-derived feature stacks

Required local inputs:

```text
Outputs/Spectral_Indices/2018/FeatureStack_2018_8bands.tif
Outputs/Spectral_Indices/2026/FeatureStack_2026_8bands.tif
```

Expected: EPSG:32645, 3 m pixels, common extent/transform, 8 bands ordered Blue, Green, Red, NIR, NDVI, NDWI, GNDVI, Brightness.

The feature-stack-generation notebook was not in the uploaded archive and is therefore documented as an input rather than reconstructed from assumptions.

## Training / development-validation samples

```text
Samples/Rajshahi_RF_Samples_QC_Corrected.gdb
```

Required layers: `Training_2018`, `Validation_2018`, `Training_2026`, `Validation_2026`; label field: `Class_ID` (1 Built_up, 2 Vegetation_Cropland, 3 Bare_Open_land, 4 Waterbody).

## Common river/sandbar exclusion

Expected by the built-up change notebook as either:

```text
Samples/Common_River_Sandbar_Mask_3m.tif
Samples/Common_River_Sandbar_Mask.shp
```

## Current OSM road network

```text
Data/Road_Network/Rajshahi_OSM_Roads_Current.gpkg
```

Record the extraction/download date and source before permanent archival release.

## Final independent test points

Notebook 05 generates the map-stratified sample. `Ref_ID` must be interpreted manually from date-matched source imagery before notebook 06 is run. The classified map must not be used as the reference source.


## 6. Sentinel-2 cross-sensor robustness inputs

Raw seasonal exports expected after running the GEE script:

```text
Data/Sentinel2/2018/S2_2018_BGRNIR_SR_Rajshahi_10m_EPSG32645.tif
Data/Sentinel2/2026/S2_2026_BGRNIR_SR_Rajshahi_10m_EPSG32645.tif
```

Expected properties:

- source collection: `COPERNICUS/S2_SR_HARMONIZED`
- temporal window: 1 March–30 April in each year
- bands: Blue, Green, Red, NIR
- scale: 10 m
- CRS: EPSG:32645
- reflectance scaling: 0.0001
- NoData: -9999
- SCL-based cloud/shadow masking

The exact adapted reference set used by the reported Sentinel-2 robustness run is included as:

```text
Samples/Sentinel2_RF_Samples_Adapted.gpkg
```

Required layers:

```text
Training_2018
Validation_2018
Training_2026
Validation_2026
Augmented_Training_Review_2018
Augmented_Training_Review_2026
```

Notebook 12 reconstructs the archived selection from the previously interpreted reference pool and performs distance/valid-pixel QA.

## 7. Inputs required for the common-domain cross-sensor comparison

```text
Outputs/RF_Context_Correction/2018/RF_LULC_2018_context_final.tif
Outputs/RF_Context_Correction/2026/RF_LULC_2026_context_final.tif
Outputs/Sentinel2_RF_Adapted/2018/S2_RF_LULC_2018.tif
Outputs/Sentinel2_RF_Adapted/2026/S2_RF_LULC_2026.tif
Samples/Common_River_Sandbar_Mask_3m.tif
```

The river/sandbar mask convention used by notebook 14 is:

```text
non-zero = excluded river/sandbar
0 = retained analytical land
```

Verify this coding before a publication-final rerun.
