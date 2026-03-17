# Time Series & Panel Data Analysis

**Author:** Dylan Jeon
**Date:** March 6, 2025

---

## Overview

This project is split into two parts:

- **Part 1** — Time series modeling of **Life Expectancy** and **Unemployment** using AR, ARDL, and VAR models
- **Part 2** — Panel data analysis of **Economic Growth** determinants using Pooled OLS, Fixed Effects, and Random Effects models

---

## Repository Structure
```
├── Time_Series_Analysis.Rmd   # Full R Markdown source
├── Time_Series_Analysis.md    # Knitted GitHub output
├── life.csv                   # Life expectancy & socioeconomic dataset
├── Economic Indicators And Inflation.csv  # Panel data dataset
└── README.md
```

---

## Part 1: Time Series Modeling

### Variables

| Type | Variable |
|---|---|
| Response | Life Expectancy (World Bank) |
| Response | Unemployment Rate (%) |
| Predictor | Health Expenditure (% of GDP) |
| Predictor | Prevalence of Undernourishment (%) |
| Predictor | Education Expenditure (% of GDP) |

### Methods

- Stationarity testing via ADF test and ACF/PACF plots
- AR(1) and AR(2) models for each response variable
- ARDL(1,1) and ARDL(2,2) models with selected predictors
- VAR(4) model capturing interactions between Life Expectancy and Unemployment
- Granger causality tests, Impulse Response Functions (IRF), FEVD, and CUSUM stability test

### Key Results

| Variable | Best Model | Test RMSE |
|---|---|---|
| Life Expectancy | AR(2) | 8.63 |
| Unemployment | VAR(4) | 6.56 |

- AR(2) was preferred for Life Expectancy based on lower AIC (22740.73 vs. 22765.38)
- VAR(4) was preferred for Unemployment as it captures interdependencies between both series
- ARDL models showed near-perfect collinearity and were not used for final forecasting
- Weak evidence that unemployment Granger-causes life expectancy at lag 3 (p = 0.071)

---

## Part 2: Panel Data Analysis

### Variables

| Type | Variable |
|---|---|
| Response | Economic Growth (annual % change in GDP) |
| Predictor | GDP (billion USD) |
| Predictor | Inflation Rate (%) |
| Predictor | Unemployment Rate (%) |

**Panel:** 19 countries, 2010–2025 (N = 304)

### Methods

- Pooled OLS, Fixed Effects (Within), and Random Effects (Swamy-Arora) models
- Breusch-Pagan LM test to compare Random Effects vs. Pooled OLS
- Hausman test to compare Fixed vs. Random Effects

### Key Results

| Test | p-value | Conclusion |
|---|---|---|
| Breusch-Pagan LM | < 2.2e-16 | Random Effects preferred over Pooled OLS |
| Hausman Test | 0.062 | Random Effects preferred over Fixed Effects |

- **Random Effects** is the preferred model
- Inflation Rate is significant in Pooled OLS (p < 0.001) but not under panel models, suggesting the effect is driven by between-country variation
- GDP and Unemployment Rate are not significant across any model specification

---

## Requirements
```r
install.packages(c(
  "forecast", "tseries", "caret", "dynlm", "ggplot2",
  "corrplot", "dplyr", "vars", "urca", "gridExtra",
  "strucchange", "tidyverse", "plm", "lmtest", "stargazer"
))
```

---

## How to Run

1. Clone the repository
2. Place `life.csv` and `Economic Indicators And Inflation.csv` in the project root
3. Open `Time_Series_Analysis.Rmd` in RStudio and click **Knit**, or run:
```r
rmarkdown::render("Time_Series_Analysis.Rmd")
```

---

## Data Sources

- [Life Expectancy & Socioeconomic Data — World Bank via Kaggle](https://www.kaggle.com/datasets/mjshri23/life-expectancy-and-socio-economic-world-bank)
- [Economic Indicators & Inflation — Kaggle](https://www.kaggle.com/datasets/adilshamim8/economic-indicators-and-inflation)
