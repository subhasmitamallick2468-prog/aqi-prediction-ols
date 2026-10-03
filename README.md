# Air Quality Index (AQI) Prediction using OLS Regression

Predicting the Air Quality Index of an Italian city from multi-sensor chemical
readings, using Ordinary Least Squares (OLS) multiple linear regression.

Course project for **MBA652A – Statistical Modelling for Business Analytics**,
IIT Kanpur (Group 11).

## Problem

Translate raw, noisy hourly chemical-sensor readings into a single, actionable
Air Quality Index that municipal authorities could use to issue timely health
advisories.

## Dataset

- **Source:** UCI Machine Learning Repository — *Air Quality* dataset
  (hourly averaged responses from an array of metal-oxide sensors in an
  Italian city).
- **After cleaning:** 827 hourly observations used for estimation.
- Missing-value placeholders replaced with `NaN`, empty trailing rows and rows
  with missing targets dropped.

## Approach

1. **Target engineering (Y):** Built a continuous AQI score using the EPA
   piecewise breakpoint formula, mapping each pollutant concentration to its
   sub-index and taking the maximum across pollutants.
2. **Features (X):** Five metal-oxide sensor channels (CO, NMHC, NOx, NO2, O3)
   plus temperature and absolute humidity. All variables Z-score standardized
   so coefficients are comparable Beta weights.
3. **Baseline OLS:** R² = 0.849 (Adj. 0.847). Residual plots revealed
   heteroskedasticity.
4. **Diagnostics & correction:** Variance Inflation Factors exposed severe
   multicollinearity (NMHC VIF = 73.5). Backward elimination on a VIF > 5
   threshold dropped NMHC, NO2 and O3. Model re-fit with
   heteroskedasticity-consistent (robust) standard errors.
5. **Final model:** Adj. R² = 0.825 with all remaining predictors
   (CO, NOx, Temperature, Absolute Humidity) significant at p < 0.05.

## Key findings

- **CO is the dominant driver** of AQI (standardized β = 0.66) — over seven
  times the impact of temperature (β = 0.09).
- **Absolute humidity reduces AQI** (β = −0.22): dry, high-traffic days carry
  the highest risk.
- Pollution spikes at ~08:00 and 18:00–19:00 align with commute traffic,
  supporting interventions like congestion pricing or staggered hours.

## Tools

Python — pandas, statsmodels (OLS, VIF, robust standard errors), matplotlib.

## Team

Group 11 — Subhasmita Mallick, Vikram Anand, Rajdatta Kohale, Rohit Kumar Singh.

## Files

- `Group11_project1.pptx` — full presentation with charts and diagnostics.
