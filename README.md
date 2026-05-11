# Physics-Informed Solar Power Forecasting

Comparative study of machine learning, physics-informed, and hybrid deep learning approaches for solar power forecasting across diverse climates.

---

## Research Question

**Does embedding physical knowledge improve ML-based solar power forecasting?**

This project investigates whether incorporating physical solar energy relationships into machine learning pipelines can improve forecasting performance compared to purely data-driven models.

---

## Project Overview

Solar power forecasting is essential for:
- renewable energy integration
- grid stability
- energy scheduling
- smart grid optimization

This project compares three different forecasting paradigms:

1. **Pure Machine Learning**
2. **Physics-Informed Machine Learning**
3. **Hybrid Deep Learning + Physics**

The models were evaluated using weather data from:
- **Phoenix, USA** (hot desert climate)
- **Berlin, Germany** (temperate/cloudy climate)

to test robustness across contrasting environmental conditions.

---

## Methods Compared

### Method A — Direct XGBoost

A purely data-driven approach where weather and temporal features are directly mapped to AC power output using XGBoost regression.

### Method B — Physics-Informed Two-Stage Pipeline

A physics-guided forecasting framework:

Weather Features → GHI Prediction → Physics-Based PV Conversion → AC Power

This approach embeds domain knowledge into the forecasting pipeline by explicitly modeling solar irradiance and photovoltaic conversion.

### Method C — Hybrid BiLSTM Residual Learning

A hybrid architecture where:
- the physics model provides a baseline forecast
- a BiLSTM network learns residual correction patterns

This method attempts to combine:
- physical interpretability
- deep temporal learning

---

## Dataset

Weather data was collected using the NASA POWER API.

### Features Used
- Global Horizontal Irradiance (GHI)
- Temperature
- Relative Humidity
- Wind Speed
- Atmospheric Pressure
- Temporal Features (hour, day, month)

### Locations
- Phoenix, Arizona, USA
- Berlin, Germany

### Temporal Resolution
Hourly data

---

## Evaluation Metrics

The following forecasting metrics were used:

- RMSE (Root Mean Squared Error)
- nRMSE (Normalized RMSE)
- MAE (Mean Absolute Error)
- MBE (Mean Bias Error)
- R² Score

Statistical significance between forecasting models was evaluated using the **Diebold-Mariano (DM) Test**.

---

## Final Results

| Method | RMSE (W) | nRMSE (%) | MAE (W) | R² |
|---|---:|---:|---:|---:|
| Persistence Baseline | 3542.36 | 46.82 | 2877.56 | -1.95 |
| Method A — Direct XGBoost | 879.96 | 11.63 | 662.19 | 0.818 |
| Method B — Two-Stage Physics | **848.39** | **11.21** | **650.47** | **0.831** |
| Method C — Hybrid BiLSTM | 1319.14 | 17.44 | 992.83 | 0.591 |

---

## Per-Location Performance

### Phoenix (4,404 samples)

| Method | RMSE (W) | R² |
|---|---:|---:|
| Method A | 958.4 | 0.7985 |
| Method B | **940.5** | **0.8060** |
| Method C | 1653.4 | 0.4003 |

### Berlin (4,404 samples)

| Method | RMSE (W) | R² |
|---|---:|---:|
| Method A | 786.9 | 0.7362 |
| Method B | **738.3** | **0.7677** |
| Method C | 833.0 | 0.7043 |

---

## Statistical Comparison (Diebold-Mariano Test)

| Comparison | DM Statistic | p-value | Significant |
|---|---:|---:|---:|
| A vs B | 4.7258 | 0.0000 | YES |
| A vs C | -22.0184 | 0.0000 | YES |
| B vs C | -23.2248 | 0.0000 | YES |

The results indicate that performance differences between forecasting approaches are statistically significant.

---

## Key Findings

- Physics-informed modeling improved forecasting accuracy over pure ML.
- The two-stage physics-guided pipeline achieved the best overall performance.
- Hybrid residual learning showed inconsistent generalization across climates.
- All ML approaches significantly outperformed persistence forecasting.
- Statistical significance was validated using Diebold-Mariano tests.

---

## Visualizations

## Exploratory Data Analysis (EDA)

EDA was performed to understand weather patterns and solar power behavior across different climates.

![EDA Analysis](Figures/Figures.png)
---

## Repository Structure

```text
physics-informed-solar-forecasting/
│
├── solar_forecasting.ipynb
├── README.md
├── requirements.txt
│
├── figures
├── results/
│   └── metrics.csv
│
└── data/
    └── sample_data.csv
