# PJM Energy Forecast for Decisions

A CFO needs to budget energy costs 12 months out. Energy prices are volatile. A point estimate is not enough — it creates false precision that leads to under-reserving when prices spike, or over-reserving and tying up capital unnecessarily.

This project produces a forecast with prediction intervals, aggregated to monthly and annual figures, so a CFO can set reserves based on a range of plausible outcomes rather than a single number.

---

## The Cost of Being Wrong

Under-reserving when prices spike means drawing from contingency funds or absorbing an unplanned hit to margins. Over-reserving means capital sitting idle that could have been deployed elsewhere. Both directions have a real cost.

---

## Why This Framing

At Novo Nordisk I built a long-term reagent demand forecast to support strategic planning in Quality Control. The business problem was structurally the same: decision-makers needed a forward-looking view with quantified uncertainty, not a point estimate, so they could make resource commitments with an appropriate buffer built in.

The energy cost budgeting problem is the same problem in a different domain.

---

## What This Project Delivers

- A time series forecast of daily wholesale electricity prices at the PJM West hub
- Prediction intervals at 80% and 95% confidence, aggregated to monthly and annual budget figures
- Output framed for a CFO, not a data scientist

---

## What This Project Does Not Deliver

- Intraday or real-time price forecasting
- Procurement timing recommendations (when to hedge vs. spot market)
- Load-shifting or demand-side optimisation
- A production-ready deployed model

---

## Data Sources

| Source | Description | Granularity | Coverage |
|---|---|---|---|
| PJM via Kaggle | Hourly energy consumption in MW | Hourly | 2002–2018 |
| EIA via ICE | Wholesale spot price at PJM West hub ($/MWh), volume-weighted daily average | Daily | 2001–2018 |

See `data/README.md` for download instructions.

---

## Notebooks

| Notebook | Purpose |
|---|---|
| `00_data_ingestion.ipynb` | Fetch and validate all data sources |
| `01_eda.ipynb` | Explore, clean, and understand the data |
| `02_modelling.ipynb` | Build forecast, evaluate, and produce CFO-facing output |

---

## Out of Scope

Excluded to keep this project finishable:

- Intraday (hourly) price modelling
- Weather data as an exogenous variable
- Procurement hedging strategy optimisation
- Multi-region analysis beyond PJM West

---

## Definition of Done

This project is complete when:

1. All three notebooks run end-to-end without errors on a clean environment
2. The modelling notebook produces a 12-month price forecast with prediction intervals
3. The final output is interpretable by a non-technical reader
4. `data/README.md` contains sufficient instructions to reproduce the data environment

---

## Setup

See `data/README.md` for data download instructions and `requirements.txt` for dependencies.
