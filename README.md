# Retail Demand & Inventory Intelligence Platform

A Microsoft Fabric portfolio project demonstrating a retail lakehouse workflow, demand forecasting, and Power BI decision support.

> **Prototype and accuracy note:** The 28-day seasonal-mean baseline reports MAE 1.0463, RMSE 2.1880, and WAPE 75.46% on a 28-day holdout. The WAPE indicates substantial forecast error. Inventory risk, safety-stock, and replenishment outputs are demand-based proxies because actual on-hand inventory and supplier lead times are unavailable. Revenue is partial because 12,299,413 historical rows had missing prices.

## Repository guide

- [`Notebooks/`](Notebooks/) — exported Fabric notebooks for Silver transformations, forecasting, and model preparation.
- [`Pipeline/`](Pipeline/) — the exported `Retail_Data_Quality_Pipeline` definition and notes. This pipeline runs the data-quality notebook; it is separate from the ETL transformations notebook.
- [`Model/`](Model/) — semantic-model screenshots and a table, relationship, and measure inventory.
- [`Power BI/`](Power%20BI/) — the Power BI report backup; its README explains the live workspace connection.
- [`Docs/project_notes.md`](Docs/project_notes.md) — project overview, architecture, limitations, and backup notes.
- [`Docs/forecasting_methodology.md`](Docs/forecasting_methodology.md) — baseline method, holdout metrics, and interpretation.

## Current backup scope

This backup includes `Retail_ETL_Transformations.ipynb`, `Day05_Demand_Forecasting.ipynb`, `Day06_Model_Preparation.ipynb`, and `Day02_03_PySpark_Exploration.ipynb`. It does **not** include an export of `Day04_Data_Quality_Checks`; the pipeline references that notebook by Fabric ID. The backup is therefore useful for review but does not contain every asset needed to independently restore or rerun the full workspace.

The source CSVs are not included. Check the source dataset's attribution and license before sharing or redistributing data. Fabric-specific settings and object IDs may need to be configured for a different workspace.

