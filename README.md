# Nigeria Crop Recommendation with Live Climate Data

A machine learning pipeline that predicts suitable crops for different Nigerian locations by combining a trained Random Forest classifier with real-time climate data pulled from NASA's POWER API.

## Overview

This project extends a standard crop recommendation ML model by feeding it live, location-specific climate data instead of static dataset values. It pulls real temperature, humidity, and rainfall data for several Nigerian cities/states and compares the model's crop recommendations across Nigeria's climate gradient, from the humid southwest to the drier north.

## What it does

1. Trains a Random Forest classifier on a crop recommendation dataset (soil nutrients N/P/K, temperature, humidity, pH, rainfall → recommended crop)
2. Pulls real annual climate data (temperature, humidity, rainfall) for six Nigerian locations (Lagos, Ogun, Kano, Kaduna, Benue, Ondo) using NASA's POWER API — no authentication required
3. Feeds the live climate data into the trained model alongside representative soil values to generate location-specific crop recommendations
4. Visualizes and compares rainfall and recommendations across locations

## A real debugging case study

While building this, the initial rainfall values pulled from the API appeared unrealistically low. Investigation revealed that NASA POWER's climatology endpoint returns rainfall as an **average daily rate (mm/day)**, not an annual total — a common unit-interpretation pitfall in geospatial data work. The fix (multiplying by 365) was validated against known real-world rainfall figures for Nigeria, and the corrected output matched Nigeria's actual climate pattern closely (~1,500-1,600mm in the southwest, dropping to ~600mm in the north). This case is documented in the notebook as a practical example of why validating data units against domain knowledge matters.

## Tech stack

- Python
- pandas (data handling)
- scikit-learn (Random Forest classifier)
- requests (NASA POWER API calls)
- Matplotlib (visualization)

## Important limitation

The underlying crop recommendation model was trained on an Indian agricultural dataset (ICFA/ICAR soil-climate-crop relationships), not Nigerian data. This project should be read as a demonstration of **methodology** — combining a trained ML model with live geospatial climate data — rather than as agronomically valid crop advice for Nigerian farmers. A production-ready version would require retraining on Nigerian soil survey and crop yield data.

## Data sources

- Crop Recommendation Dataset (soil/climate/crop labels)
- NASA POWER API (https://power.larc.nasa.gov/) — live climatology data, no authentication required

## Next steps

- Source Nigerian-specific soil and crop yield data (e.g., from IITA or state ministries of agriculture) to retrain the model for genuine local validity
- Extend from six sample locations to a full spatial grid across Nigeria for a mapped crop suitability output
- Incorporate soil nutrient data from a real source rather than assumed representative values

## Author

Adebayo — Postgraduate researcher in GIS and remote sensing, Federal University of Technology, Akure (FUTA)
