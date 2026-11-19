# Traffic-Volume-Forecasting
72-hour traffic volume forecasting using R, exponential smoothing and regression-based models, with rolling evaluation and prediction intervals.
# Traffic Volume Forecasting | 72-Hour Ahead Analysis

**Academic Group Project | Time Series Forecasting · Predictive Analytics · Logistics**

**Tools:** R  
**Methods:** Exponential Smoothing (ETS), Linear Regression, Seasonal ARIMA Errors, Rolling-Window Evaluation, Bootstrap Prediction Intervals

## Project Overview

This project investigates how hourly traffic-volume forecasts can support advance delivery scheduling and logistics planning. It was developed as an **academic case study**, using a *fictional* consulting and logistics scenario rather than a commissioned client engagement.

The team compared forecasting approaches for traffic on westbound Interstate 94 near Minneapolis–St. Paul, with a **72-hour forecast horizon**. The business objective was to explore how predicted traffic patterns could help inform delivery timing and congestion-aware planning.

## Objectives

- Understand recurring daily and weekly traffic patterns.
- Compare simple exponential smoothing, a seasonal ETS model, linear regression and regression with seasonal ARIMA errors.
- Evaluate out-of-sample point forecasts across a 72-hour horizon.
- Assess the empirical coverage and sharpness of 95% bootstrap prediction intervals.

## Dataset

The study used a processed subset of the **Metro Interstate Traffic Volume** dataset, originally published through the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/492/metro+interstate+traffic+volume).

| Study characteristic | Value |
| --- | --- |
| Observation frequency | Hourly |
| Study period | January 2016 – September 2018 |
| Observations used in project | 24,096 |
| Forecast horizon | 72 hours |
| Rolling training window | 17,544 hours |
| Rolling forecast origins | 6,481 |

The source UCI dataset is larger than the project's prepared subset. The script expects a locally prepared `TheOutliers_Data.csv`, **not the original UCI CSV directly**. That input file is not included in this repository.

## Analytical Approach

**Exploratory data analysis.** Examined daily and weekly seasonality, including contrasting weekday and weekend traffic profiles.

**Model development.** Compared simple exponential smoothing (SES), additive Holt–Winters/ETS, a linear model (LM) with hour-by-weekend interactions, and the LM extended with seasonal ARIMA errors. Weather variables were explored, but lagged temperature did not improve the fitted regression-plus-ARIMA approach in the reported analysis.

**Rolling evaluation.** Evaluated 72-step-ahead predictions using a fixed-length training window advanced by one hour at each forecast origin. Point accuracy was compared using mean squared error (MSE), with Diebold–Mariano tests applied to selected model comparisons.

**Prediction intervals.** Assessed nominal 95% bootstrap prediction intervals using unconditional coverage and the Winkler score.

## Selected Findings

- **Daily and weekly seasonality:** Traffic volume displayed pronounced 24-hour and 168-hour patterns, with different hourly profiles on weekdays and weekends.
- **Point forecast accuracy:** In the reported out-of-sample comparison, the **linear regression model (LM)** achieved the lowest average MSE across the 72 forecast horizons. The single-seasonal ETS approaches deteriorated at longer horizons.
- **Prediction intervals:** The report found that the ETS intervals did not achieve the target 95% coverage, whereas the LM-based bootstrap intervals were better calibrated. Comparisons of the LM and LM-with-SARIMA intervals varied by forecast horizon.
- **Operational interpretation:** Explicit modelling of the hour of day and weekend effects proved valuable for this forecasting exercise. Calendar events and traffic incidents were identified as possible future extensions.

The findings are specific to the chosen study period, models and evaluation design; they do not establish that one method is universally best for traffic forecasting.

## Project Files

- [Project presentation (PDF)](presentation.pdf) — objectives, methods, graphics and results
- [Full academic report (PDF)](report.pdf) — detailed explanation and evaluation
- [R analysis script](analysis/Project_forecasting.R) — original analytical workflow with two clearly documented corrections to bootstrap storage variable names
- [Code and reproducibility notes](analysis/README.md)

**Reproducibility note:** The prepared data are absent. The R script has not been rerun to independently regenerate the published results for this GitHub version. It is shared as documentation of the original group work, not as a verified end-to-end reproducible pipeline.

## Dataset Credit

Hogue, J. (2019). *Metro Interstate Traffic Volume* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5X60B. The UCI dataset is distributed under CC BY 4.0.

## Project Context and Credits

**University of Bologna — Forecasting and Predictive Analytics (2024/2025)**  
**Group members:** Lisa Rigo, Paola D'Amore and Jacopo Malaguti.

BrightPath Consulting and EverTrack Logistics are **fictional organisations used in the classroom business scenario**. This repository is an academic portfolio presentation, not evidence of professional work for those companies.
