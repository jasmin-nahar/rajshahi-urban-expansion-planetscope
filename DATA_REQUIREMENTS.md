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
