# 🌍 Climate & Health Spatial–Temporal Modelling in Rwanda

**Lead:** Dr. Similien Ndagijimana  
**Affiliation:**  HISP Rwanda|Ministry of Health Rwanda 
**Project:** Rwanda – Climate & Health Initiative (Malaria Use case)

---

## Project Overview

This repository contains the full modelling pipeline for spatial and spatio-temporal analysis of climate-sensitive diseases in Rwanda.

The project integrates:

- Routine Health Information System (RHIS) data
- Climate and environmental data (rainfall, temperature, NDVI, PM2.5)
- Sector-level spatial data (416 sectors)
- Bayesian hierarchical modelling (INLA framework)

### Objectives

- Estimate sector-level Relative Risk (RR)
- Quantify spatial and temporal disease patterns
- Assess climate–disease associations
- Generate short-term forecasts
- Support early warning systems
- Integrate outputs into DHIS2 dashboards

## Modelling Framework

We use a Bayesian hierarchical spatio-temporal model:

### Likelihood

\[
Y_{it} \sim Poisson(E_{it} \lambda_{it})
\]

Where:

- \(Y_{it}\) = observed cases in sector *i* at time *t*
- \(E_{it}\) = expected cases (population offset)
- \(\lambda_{it}\) = relative risk

---

### Linear Predictor

\[
\log(\lambda_{it}) =
\alpha
+ u_i
+ v_i
+ \gamma_t
+ \delta_{it}
+ \beta X_{it}
\]

Where:

- \(u_i\) = structured spatial effect (CAR/BYM2)
- \(v_i\) = unstructured spatial effect (IID)
- \(\gamma_t\) = temporal trend (RW1 or RW2)
- \(\delta_{it}\) = space-time interaction
- \(X_{it}\) = climate covariates

---

## Spatial Component

We use the **BYM2 parameterization** with:

- Scaled spatial model
- Penalized Complexity (PC) priors
- Adjacency matrix (`Adj_Map.graph`)
- Shapefile: `rwa_adm3_2006_NISR_WGS1984_20181002.shp`

---

## Temporal Component

- Random Walk 1 (RW1)
- Random Walk 2 (RW2)
- Monthly seasonality (optional)
- Lagged climate effects

## Climate Covariates

- Rainfall (ERA5-Land)
- Temperature (ERA5-Land)
     -Max Temperature
     -Min Temperature
     -Air Temperature
- Relative Humidity
- NDVI
- Lag structures (0–3 months tested)

---

## Model Evaluation

Model comparison metrics:

- WAIC
- DIC
- CPO
- PIT histograms

Risk classification based on:

- Posterior probability \(P(RR > 1)\)

---

## Forecasting

Predictions are generated as:

\[
\hat{Y}_{i,t+h} \sim Poisson(E_{i,t+h} \hat{\lambda}_{i,t+h})
\]

Outputs include:

- Mean forecast
- 95% predictive intervals
- Early warning thresholds

---

## Repository Structure

