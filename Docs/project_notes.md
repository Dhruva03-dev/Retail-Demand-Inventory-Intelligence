# Retail Demand & Inventory Intelligence Platform

## Project overview

This Microsoft Fabric portfolio project transforms historical retail sales data into curated analytics tables, a short-horizon demand forecast, and Power BI decision-support views. It demonstrates a lakehouse workflow from Bronze ingestion through Silver and Gold modeling, forecasting, semantic modeling, and reporting.

**Workspace:** `Retail Demand Intelligence`  
**Lakehouse:** `RetailLakehouse`  
**Transformation notebook:** `Retail_ETL_Transformations`  
**Forecast notebook:** `Day05_Demand_Forecasting`  
**Data-quality notebook:** `Day04_Data_Quality_Checks`  
**Backed-up pipeline:** `Retail_Data_Quality_Pipeline`

> **Portfolio prototype.** Inventory risk, safety stock, and replenishment outputs are demand-based proxies. The source data has no actual on-hand inventory or supplier lead times, so these outputs do not confirm stockouts or represent operational purchase recommendations.

## Business purpose

The platform supports exploration of historical sales, comparison of a 28-day demand forecast with actual demand, and review of item–store combinations that may warrant attention. It demonstrates an analytics workflow and decision support; it is not a production inventory planning system.

## Data flow and assets

### Bronze: source-shaped CSVs

The Fabric project uses these source files:

- `calendar.csv`
- `sales_train_validation.csv`
- `sell_prices.csv`

The source CSVs are not included in this backup. Confirm attribution and license terms before sharing or redistributing source data.

### Silver: transformed data

The transformation notebook is `Retail_ETL_Transformations`. The known Silver tables are:

- `silver_calendar`
- `silver_prices`
- `silver_sales` — sales reshaped to long format

### Gold: curated analytical model

The known Gold tables are:

- `gold_dim_date`
- `gold_dim_product`
- `gold_dim_store`
- `gold_fact_sales`

### Pipeline backup status

The `Pipeline` folder contains `Retail_Data_Quality_Pipeline.json` and its `manifest.json`. The pipeline definition has one `TridentNotebook` activity. The Fabric settings screenshot identifies the selected notebook as `Day04_Data_Quality_Checks` in the `Retail Demand Intelligence` workspace.

This is the **data-quality pipeline**, not the ETL orchestration pipeline. It does not run `Retail_ETL_Transformations`. The folder does not contain a `Retail_ETL_Pipeline.json` export. The `Day04_Data_Quality_Checks` notebook export is also absent from `Notebooks`, so the pipeline JSON's Fabric notebook/workspace IDs alone are not enough to restore and run it in another workspace.

The project describes data-quality checks, but the backup does not establish their exact rules, thresholds, or outcomes. Record those from notebook code and actual run evidence before claiming checks passed.

## Forecast summary

The Day 5 notebook, `Day05_Demand_Forecasting`, creates `gold_demand_forecast`. Its baseline averages demand from the four previous corresponding weekly lags: 7, 14, 21, and 28 days. It evaluates a 28-day holdout and creates a 28-day forecast. It also produces demand-based risk scoring, a safety-stock proxy, and a replenishment target proxy.

| Holdout metric | Result | Interpretation |
|---|---:|---|
| MAE | 1.0463 | Average absolute error in the forecast target's unit |
| RMSE | 2.1880 | Gives greater weight to larger misses |
| WAPE | 75.46% | Substantial error relative to total actual demand |

WAPE of 75.46% indicates substantial forecast error. Present this as a transparent baseline with room for improvement, not as production-ready performance or a guarantee of future accuracy. Exact holdout dates, scoring grain, and edge-case handling are not stated here; consult the notebook before publishing them. See [forecasting_methodology.md](forecasting_methodology.md).

## Reporting model

The Day 6 semantic model contains:

- `gold_dim_item`
- `gold_dim_store`
- `gold_dim_reporting_date`
- `gold_fact_sales`
- `gold_demand_forecast`

The model has six relationships and eight measures, documented with screenshots in [`../Model/README.md`](../Model/README.md). Exact DAX formulas and relationship settings are not included in the screenshot documentation; use an exported model definition or the live model for those details.

## Data and interpretation limitations

- **No stock position:** no on-hand inventory is available, so risk scoring cannot confirm stockouts or current stock status.
- **No supplier timing or constraints:** lead times and replenishment constraints are unavailable. Safety stock and replenishment targets are illustrative proxies without a service-level guarantee.
- **Partial revenue:** 12,299,413 historical rows had missing prices. Revenue is partial and must be labeled accordingly.
- **Forecast error:** WAPE is 75.46% on the stated holdout, reflecting substantial error. This result is specific to the reported evaluation.
- **Reproducibility:** notebooks, selected pipeline JSON, screenshots, and a PBIX are backed up, but the Day 4 quality-check notebook and a complete ETL pipeline export are missing. Do not claim full reproducibility from this folder.

## Backup inventory

The current backup contains four notebook exports, one data-quality pipeline export and manifest, a PBIX report, four semantic-model screenshots, and project/forecast documentation. It does not contain the source CSVs or the Day 4 data-quality notebook export. Fabric workspace and object identifiers in exported metadata are environment-specific.

## Recommended completion steps

1. Export `Day04_Data_Quality_Checks` into `Notebooks/` if it is part of the backup you want to retain.
2. Export the ETL orchestration pipeline if you later build or use one to run `Retail_ETL_Transformations`.
3. Capture sanitized screenshots of the report pages if you want a quick visual portfolio preview alongside the PBIX.
4. Verify source attribution and licenses before sharing the project publicly. Do not publish credentials or private workspace details.
