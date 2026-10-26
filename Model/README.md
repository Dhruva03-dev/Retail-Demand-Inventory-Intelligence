# Semantic Model

This folder documents the Day 6 Power BI semantic model for the Retail Demand & Inventory Intelligence Platform. The screenshots provide a visual record of the model structure and its current contents.

## Screenshots

| Suggested filename | What it shows |
|---|---|
| `model-diagram.png` | Model diagram with the five tables and their relationships |
| `model-tables.png` | Table inventory in the semantic model |
| `model-relationships.png` | Relationship list, including all six linked key pairs |
| `model-measures.png` | The eight measures currently listed in the model |

Use the screenshots as documentation of the visible model state. They are not a substitute for an exported model definition if one is available.

## Tables

The model contains these five tables:

- `gold_demand_forecast`
- `gold_dim_item`
- `gold_dim_reporting_date`
- `gold_dim_store`
- `gold_fact_sales`

## Relationships

The relationship list shows six links:

| One-side table and key | Many-side table and key |
|---|---|
| `gold_dim_reporting_date[date]` | `gold_demand_forecast[forecast_date]` |
| `gold_dim_item[item_id]` | `gold_demand_forecast[item_id]` |
| `gold_dim_store[store_id]` | `gold_demand_forecast[store_id]` |
| `gold_dim_reporting_date[date]` | `gold_fact_sales[date]` |
| `gold_dim_item[item_id]` | `gold_fact_sales[item_id]` |
| `gold_dim_store[store_id]` | `gold_fact_sales[store_id]` |

The screenshots show the dimensions on the `1` side and the forecast and sales tables on the `*` side. Refer to the live model for any relationship settings not visible in these screenshots.

## Measures

The model lists these eight measures:

- Average Inventory Risk Score
- Average Safety Stock Proxy
- Forecast Units
- Forecasted Replenishment Target
- High-Risk Forecast Rows
- Historical Sales Rows
- Known-Price Revenue
- Total Units Sold

The screenshots document measure names, not their DAX definitions. Add formulas and detailed definitions only from the semantic model itself.

## Interpretation notes

- `Known-Price Revenue` is partial because 12,299,413 historical rows had missing prices. Label it as partial wherever it appears in the report.
- Inventory risk, safety stock, and replenishment values are demand-based proxies. The source data has no actual on-hand inventory or supplier lead-time information, so these measures do not establish stockout status or provide operational purchase recommendations.
- The forecast's reported holdout WAPE is 75.46%, indicating substantial forecast error. See the forecasting methodology document for the metric context.

## Updating this folder

When the model changes, replace the screenshots with current, legible captures and update this README if tables, relationships, or measure names change. Do not include workspace credentials, private endpoints, or sensitive account details in the images.
