# Forecasting methodology

## Purpose and scope

The Day 5 notebook, `Day05_Demand_Forecasting`, creates `gold_demand_forecast` with a 28-day demand forecast. It uses an interpretable four-week seasonal mean baseline and evaluates it on a 28-day holdout. The reported figures below are the supplied project results; consult the notebook run and outputs for the exact evaluation dates and implementation details.

## Baseline

For a forecasted day, the baseline averages demand from the four corresponding weekly lags:

- 7 days earlier
- 14 days earlier
- 21 days earlier
- 28 days earlier

In compact form, if `y(t)` is demand on day `t`, the stated baseline is:

`forecast(t) = mean(y(t-7), y(t-14), y(t-21), y(t-28))`

This captures a recurring weekly pattern using the previous four matching weekdays. It is a simple reference method, not a fitted machine-learning model. The project summary does not specify how the notebook handles missing lag values, negative values, zero-demand series, new items, or incomplete history; verify those behaviors in the notebook before documenting them as facts.

## Holdout results

| Metric | Result | Definition and interpretation |
|---|---:|---|
| MAE | 1.0463 | Mean absolute difference between actual and predicted demand, in the target's unit |
| RMSE | 2.1880 | Square root of mean squared error; larger misses contribute more heavily |
| WAPE | 75.46% | Sum of absolute errors divided by total actual demand, expressed as a percentage |

A WAPE of 75.46% means the total absolute forecast error is large relative to actual demand over this evaluation. This is substantial forecast error. Describe the result as a transparent baseline with substantial room for improvement. Do not call it production-ready, generalize it beyond the evaluated holdout, or imply that it guarantees better inventory outcomes.

The supplied facts do not identify the holdout start/end dates, exact scoring grain, filtering/exclusions, or zero-total-demand handling. Do not invent these details. If publishing a reproducibility appendix, extract and record them from the notebook and its run evidence.

## Forecast-derived decision support

The notebook also produces demand-based risk scoring, a safety-stock proxy, and a replenishment target proxy. These should be interpreted only as exploratory signals derived from forecast demand. The project has no actual on-hand inventory, supplier lead times, or stated replenishment constraints. Therefore:

- Risk scoring is not a confirmed stockout prediction.
- Safety stock is not a service-level-calibrated inventory policy.
- Replenishment target is not a purchase order or operational recommendation.

## What to verify for a technical release

Use the notebook and model artifacts to fill in details only when they are documented there:

- Target column, forecast grain, training cutoff, and exact holdout dates
- How predictions are produced for each of the 28 forecast days
- Treatment of missing lag values, nulls, negative values, zero-demand items, and cold starts
- Whether metrics are pooled across all scored rows or averaged per series
- WAPE behavior when total actual demand is zero
- Any filters, exclusions, and rows included in the score
- Forecast output columns and the exact formulas/thresholds for risk, safety stock, and replenishment proxy

Keep the reported metrics unchanged unless a documented rerun replaces them. If values change, record the run date and the corresponding notebook version or commit.
