# Data

## PJM Hourly Energy Consumption

**Source:** Kaggle — robikscube/hourly-energy-consumption  
**URL:** https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption  
**Version:** v3  
**Downloaded:** 2026-05-31   
**Granularity:** Hourly  
**Coverage:** 2002–2018  
**File(s) used:** `PJMW_hourly.csv`

### Download instructions
Requires the Kaggle API and credentials in `.env` as `KAGGLE_USERNAME` and `KAGGLE_KEY`.
Run `notebooks/00_data_ingestion.ipynb` from top to bottom.

---

## EIA Wholesale Spot Prices — PJM West

**Source:** U.S. Energy Information Administration, republished from ICE  
**URL:** https://www.eia.gov/electricity/wholesale  
**Downloaded:** 2026-05-31   
**Granularity:** Daily (volume-weighted average price in $/MWh)  
**Coverage:** 2001–2018  
**Hub used:** PJM WH Real Time Peak  
**File(s) used:**
- `ice_electric-historical.zip` (2001–2013, extracted manually)
- `ice_electric-2014final.xls`
- `ice_electric-2015final.xls`
- `ice_electric-2016final.xls`
- `ice_electric-2017final.xls`
- `ice_electric-2018final.xlsx`

### Download instructions
EIA blocks automated downloads. Download files manually from the URL above
and place them in `data/raw/`. The historical zip should be extracted in place.

---

## Notes

- Raw files are gitignored and must be downloaded before running any notebook.
- Processed outputs are saved to `data/processed/` as parquet files and are also gitignored.
- All file versions above were current as of the download date. If reproducing this
  work at a later date, verify that the EIA files have not been revised.