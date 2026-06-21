# SpatialLagXJatim
This project analyzes the spatial relationship between socioeconomic indicators and poverty levels across districts/cities in Central Java (Jawa Tengah), Indonesia, using a **Spatial Lag X (SLX) regression model**.

## Overview

Standard OLS regression often ignores spatial dependence between neighboring regions. This project incorporates spatial effects by adding spatially-lagged independent variables (WX) to the model, testing whether conditions in neighboring districts influence poverty in a given district.

## Data

- **Geospatial boundary data**: `Jawa Tengah.zip` — shapefile of Central Java district/city boundaries
- **Socioeconomic data**: `Spasial_Jawa_Tengah_Cleaned.xlsx` — cleaned indicator data per district/city

## Variables

| Variable | Description |
|---|---|
| `Y` | Poverty rate (dependent variable) |
| `RLS` | Mean Years of Schooling (*Rata-rata Lama Sekolah*) |
| `AHH` | Life Expectancy (*Angka Harapan Hidup*) |
| `TPT` | Open Unemployment Rate (*Tingkat Pengangguran Terbuka*) |
| `APD` | *(describe this indicator here)* |
| `WX_*` | Spatially-lagged version of each predictor |

## Workflow

1. **Import & Load Data** — load shapefile and indicator dataset, merge on district/city
2. **Descriptive Statistics** — explore distributions of dependent and independent variables
3. **Spatial Weight Matrix** — construct using Haversine distance between district centroids, with row-standardization (Queen contiguity also explored)
4. **Moran's I Test** — test for spatial autocorrelation in the variables to justify a spatial model
5. **Spatial Lag X (SLX) Model** — fit OLS regression including spatially-lagged predictors (`WX_RLS`, `WX_AHH`, `WX_TPT`, `WX_APD`)
6. **Diagnostics**:
   - Kolmogorov-Smirnov test for residual normality
   - Variance Inflation Factor (VIF) for multicollinearity
7. **Revision** — outlier handling and model refinement based on initial Moran's I and diagnostic results, followed by re-estimation

## Tools & Libraries

- `geopandas`, `pandas`, `numpy`
- `libpysal`, `esda`, `splot` (spatial weights, Moran's I)
- `statsmodels` (OLS regression, VIF)
- `scipy` (Haversine distance, KS test)
- `matplotlib`

## How to Run

```bash
pip install geopandas pandas numpy libpysal esda splot statsmodels scipy matplotlib
```

Open and run `Spasial_LagX_FINAL.ipynb` in Jupyter or Google Colab. Make sure `Jawa Tengah.zip` and `Spasial_Jawa_Tengah_Cleaned.xlsx` are in the working directory.

## Results

The final SLX model includes `RLS`, `AHH`, `TPT`, `APD`, and their spatial lags as predictors of poverty rate, with diagnostics confirming normally distributed residuals and acceptable multicollinearity levels after revision.

## License

*(add your license here, e.g. MIT)*
