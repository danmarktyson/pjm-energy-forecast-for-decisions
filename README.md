# PJM Energy Forecast for Decisions

Data centres are one of the fastest-growing sources of electricity demand in the US. Running one is capital-intensive, and electricity is among the largest operating costs. A CFO at a data centre operator connected to the PJM grid needs to budget energy costs 12 months out. Energy prices are volatile. A point estimate is not enough: it creates false precision that leads to under-reserving when prices spike, or over-reserving and tying up capital unnecessarily.

This project produces a 12-month wholesale electricity price forecast with prediction intervals for the PJM West hub. The output is in $/MWh. A CFO applies their own consumption volume to convert that into a dollar budget figure.

---

## The Decision-Maker

A CFO at a data centre operator drawing power from the PJM grid. PJM is the regional transmission organisation that operates the electricity market across 13 US states and Washington D.C., one of the largest competitive wholesale electricity markets in the world.

The CFO does not operate the grid. They buy from it. What they need to know is what that is likely to cost over the next year, and how wrong that estimate could plausibly be.

---

## The Cost of Being Wrong

Electricity typically represents 20-40% of total data centre operating costs, varying by facility size and workload type ([IAEI Magazine, 2025](https://iaeimagazine.org/electrical-fundamentals/how-much-electricity-does-a-data-center-use-complete-2025-analysis/); [The Network Installers, 2026](https://thenetworkinstallers.com/blog/data-center-operating-costs/)). Under-reserving when prices spike means drawing from contingency funds or absorbing an unplanned hit to margins. Over-reserving means capital sitting idle that could have been deployed elsewhere. At that share of operating expenditure, the cost of being wrong in either direction is significant.

---

## Why This Framing

At Novo Nordisk I built a long-term reagent demand forecast to support strategic planning in Quality Control. The business problem was structurally the same: decision-makers needed a forward-looking view with quantified uncertainty, not a point estimate, so they could make resource commitments with an appropriate buffer built in.

The energy cost budgeting problem is the same problem in a different domain.

---

## What This Project Delivers

- A 12-month wholesale electricity price forecast for the PJM West hub in $/MWh, aggregated to monthly and annual figures with prediction intervals at 80% and 95% confidence
- A comparison against a seasonal naive benchmark, quantifying the business value of the forecasting approach in dollar terms
- Output framed for a CFO, not a data scientist

The forecast is expressed in $/MWh. A CFO multiplies this by their facility's expected consumption to arrive at a total energy budget. That consumption figure is specific to each operator and falls outside the scope of this project.

---

## What This Project Does Not Deliver

- Intraday or real-time price forecasting
- Procurement timing recommendations (when to hedge vs. spot market)
- Load-shifting or demand-side optimisation
- A production-ready deployed model

---

## Data Sources

| Source | Description | Role | Granularity | Coverage |
|---|---|---|---|---|
| PJM via Kaggle | Hourly energy consumption in MW | Candidate feature for price modelling | Hourly | 2002-2018 |
| EIA via ICE | Wholesale spot price at PJM West hub ($/MWh), volume-weighted daily average | Forecast target | Daily | 2001-2018 |

See `data/README.md` for download instructions.

---

## Notebooks

| Notebook | Purpose |
|---|---|
| `00_data_ingestion.ipynb` | Fetch and validate all data sources |
| `01_eda.ipynb` | Explore, clean, and understand the data |
| `02_modelling.ipynb` | Build forecast, evaluate, and produce CFO-facing output |
| `03_holdout_evaluation.ipynb` | Simulate real-world deployment against the 2018 holdout year |

---

## Out of Scope

Excluded to keep this project finishable:

- Intraday (hourly) price modelling
- Weather data as an exogenous variable
- Procurement hedging strategy optimisation
- Multi-region analysis beyond PJM West

---

## Real-World Holdout

The final year of data (2018) is withheld from all EDA and modelling work. Once
the model is built and evaluated on the preceding years, it is run against 2018
as a simulation of real-world deployment: the model sees only what it would have
known at the end of 2017 and forecasts into a year it has never seen. This tests
whether the model holds up under conditions that resemble practice rather than
a controlled experiment.

---

## Definition of Done

This project is complete when:

1. All four notebooks run end-to-end without errors on a clean environment
2. The modelling notebook produces a 12-month price forecast with prediction intervals
3. The final output is interpretable by a non-technical reader
4. `data/README.md` contains sufficient instructions to reproduce the data environment
5. The 2018 holdout evaluation is complete and results are discussed in plain language

---

## Setup

See `data/README.md` for data download instructions and `requirements.txt` for dependencies.
