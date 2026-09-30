# Smart Reordering — Demand Forecast & Reorder Point Optimization

## Description

A feature that predicts future product demand and determines the right time to reorder stock.

## Purpose

It helps prevent stockouts and overstocking by automatically adjusting reorder levels based on demand and supplier lead times.

## How It Works

1. Collects historical sales and inventory data.
2. Forecasts future demand.
3. Considers supplier lead time.
4. Calculates safety stock and reorder point.
5. Alerts or creates a reorder recommendation when stock reaches the reorder point.

## Information Required

- Historical sales data
- Current inventory
- Supplier lead time
- Expected demand
- Safety-stock requirements
- Existing purchase orders

## Output / Action

The system provides a reorder point and recommended order quantity, and can trigger a reorder alert or purchase request.

## Benefits

- Reduces stockouts.
- Prevents unnecessary overstocking.
- Automates inventory monitoring.
- Improves purchasing decisions.

## Limitations / Dependencies

- Requires accurate sales and inventory data.
- Forecasts may be affected by sudden demand changes.
- Accurate supplier lead times are important.
- New products may have limited historical data.

## Sources

- Oracle — Reorder Point Planning
- SAP — Reorder Point Planning
- Oracle — Replenishment Planning
