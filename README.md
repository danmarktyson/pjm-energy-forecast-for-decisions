# PJM West Price Forecast: Prediction Intervals for CFO Energy Budgeting

Data centres are one of the fastest-growing sources of electricity demand in 
the US. Running one is capital-intensive, and electricity is among the largest 
operating costs. Most large operators procure electricity through long-term 
Power Purchase Agreements (PPAs) rather than directly from the spot market. 
Under a virtual PPA, the operator settles the difference between an agreed 
strike price and the prevailing wholesale market price. The wholesale price is 
therefore the benchmark that determines whether a PPA is working in the CFO's 
favour or against them.

This project produces a 12-month wholesale electricity price forecast with 
prediction intervals for the PJM West hub. The output is in $/MWh. A CFO 
applies their own consumption volume to convert that into a dollar budget figure.

---

## The Decision-Maker

A CFO at a data centre operator connected to the PJM grid. PJM is the regional 
transmission organisation that operates the electricity market across 13 US 
states and Washington D.C., one of the largest competitive wholesale electricity 
markets in the world.

The CFO's operator procures electricity through a virtual PPA with a strike 
price agreed years in advance. ([PPAs for data centres typically span 10 to 20 
years](https://www.pillsburylaw.com/en/news-and-insights/power-purchase-interconnection-agreements-data-centers.html).) 
The PPA does not eliminate the CFO's need for annual budget planning. Each year, 
the CFO must estimate the net settlement position: if wholesale prices stay below 
the strike price, the operator owes the generator the difference; if prices exceed 
it, the generator pays. A 12-month price forecast with quantified uncertainty 
gives the CFO a basis for anticipating that settlement position and setting energy 
cost reserves accordingly.

The data centre context makes this problem particularly visible right now, given 
the surge in energy demand driven by AI infrastructure. The underlying business 
problem is not unique to data centres. Any energy-intensive organisation 
operating under a PPA faces the same exposure to wholesale price movements. A 
manufacturing CFO, a pharmaceutical plant, or a large university campus would 
use this forecast in exactly the same way.

---

## The Cost of Being Wrong

[Electricity typically represents 20-40% of total data centre operating costs](https://iaeimagazine.org/electrical-fundamentals/how-much-electricity-does-a-data-center-use-complete-2025-analysis/), 
varying by facility size and workload type. Under a virtual PPA, if wholesale 
prices fall significantly below the agreed strike price, the operator compensates 
the generator for the difference, an unplanned cash outflow that the CFO needs 
to anticipate. If prices spike above the strike price, the generator compensates 
the operator, but only if the CFO understood that upside was coming. A forecast 
with prediction intervals makes that range of outcomes visible before the budget 
is set.

---

## Why This Framing

At Novo Nordisk I built a long-term reagent demand forecast to support strategic 
planning in Quality Control. The business problem was structurally the same: 
decision-makers needed a forward-looking view with quantified uncertainty, not 
a point estimate, so they could make resource commitments with an appropriate 
buffer built in.

The energy cost budgeting problem is the same problem in a different domain.

---

## What This Project Delivers

- A 12-month wholesale electricity price forecast for the PJM West hub in 
  $/MWh, aggregated to monthly and annual figures with prediction intervals 
  at 80% and 95% confidence
- A comparison against a seasonal naive benchmark, quantifying the business 
  value of the forecasting approach in dollar terms
- Output framed for a CFO, not a data scientist

The forecast is expressed in $/MWh. A CFO multiplies this by their facility's 
expected consumption to arrive at a total energy budget. That consumption figure 
is specific to each operator and falls outside the scope of this project.

The forecast operates at daily granularity rather than monthly. Daily data 
captures within-month price variation, including mid-month spikes, weekly cycles, 
and holiday effects, that disappear when data is aggregated to monthly before 
modelling. The model also trains on roughly 5,800 daily observations compared 
to 192 monthly observations across the same period, giving it substantially more 
signal when identifying seasonal patterns. To aggregate daily prediction intervals 
to monthly figures, the model generates 1,000 simulated daily price trajectories 
over the forecast horizon. Each trajectory is summed to a monthly total, and the 
resulting distribution of monthly outcomes determines the prediction intervals. 
This correctly propagates uncertainty through the aggregation rather than naively 
summing daily interval bounds, which would produce intervals that are either too 
wide or too narrow depending on the correlation structure of the errors.

---

## What This Project Does Not Deliver

- Intraday or real-time price forecasting
- Strike price optimisation or PPA negotiation recommendations
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
- Strike price optimisation or PPA negotiation recommendations
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

See `data/README.md` for data download instructions and `requirements.txt` for 
dependencies.
