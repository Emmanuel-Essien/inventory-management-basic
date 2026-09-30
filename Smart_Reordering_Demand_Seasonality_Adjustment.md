# Demand Seasonality Adjustment

## Description

Demand Seasonality Adjustment is a Smart Reordering feature that detects recurring demand patterns over time and adjusts the demand input used for replenishment decisions. Instead of treating every period as having the same expected demand, the feature identifies repeatable seasonal effects such as higher sales during particular months, weeks, days of the week, holidays, or other recurring periods.

Retail forecasting systems commonly model seasonality as a component of demand forecasting. Oracle Retail describes estimating seasonality from historical demand and using the resulting seasonal parameters together with current sales to generate forecasts.[^1]

## Purpose

The purpose is to prevent the reordering system from using a demand estimate that is systematically too low or too high during predictable seasonal periods.

For example, an item that normally sells 20 units per day but regularly sells substantially more during a particular period should not rely only on its ordinary daily demand when deciding how much stock is needed for that period. The seasonal adjustment provides information that can be passed into the existing demand forecasting and reorder-point features.

## How It Works

1. Collect historical sales or stock-out-adjusted demand for each item and location.
2. Group the observations into a suitable recurring calendar period, such as week-of-year, month, or day-of-week.
3. Compare demand in each period with the item's baseline demand.
4. Identify recurring patterns that are strong enough to be treated as seasonal rather than as a one-time spike.
5. Calculate a seasonal factor for each relevant period. A factor above 1 indicates higher-than-baseline demand, while a factor below 1 indicates lower-than-baseline demand.
6. Update the seasonal factors periodically as new demand data becomes available.
7. Combine the current baseline demand with the applicable seasonal factor when generating the demand input for the reordering process.
8. Pass the adjusted demand into the existing Demand Forecasting and Reorder Point Monitoring features.
9. If there is insufficient historical data to establish a reliable seasonal pattern, use the baseline demand without a seasonal adjustment and flag the item as having insufficient seasonal history.

## Information Required

- Item or SKU
- Location where the item is stocked
- Historical sales or demand by date
- Stock-out information, where available, so periods with constrained sales can be identified
- Calendar information such as week, month, day of week, and relevant recurring events
- Current baseline demand
- Historical seasonal factors or the data needed to calculate them
- Minimum amount of historical data required before applying a seasonal pattern

## Output / Action

- Seasonal factor for each relevant period
- Seasonally adjusted demand input
- Periods identified as having recurring higher or lower demand
- A confidence or data-sufficiency flag for the seasonal estimate
- Updated demand input passed to the existing reordering calculations

## Benefits

- Helps the system prepare for predictable changes in demand.
- Reduces reliance on one average demand figure across periods with different demand patterns.
- Makes recurring demand patterns visible to the reordering process.
- Can work alongside the existing Demand Forecasting feature rather than replacing it.
- Allows seasonal information to be updated as new sales data becomes available.

## Limitations / Dependencies

- Reliable seasonality requires enough historical observations to distinguish recurring patterns from random fluctuations.
- Promotions, stockouts, price changes, and unusual events can distort historical demand and should be considered before treating a pattern as seasonal.
- Different locations can have different seasonal patterns, so a single factor should not automatically be applied to every location.
- New products may not have enough history to establish their own seasonal pattern.
- Seasonality does not predict unexpected demand spikes, so it should be combined with other monitoring features.

## Sources

- Oracle, [Retail Inventory Planning — Forecasting Challenges and Solutions](https://docs.oracle.com/en/industries/retail/retail-inventory-planning-optimization-cloud/25.2.401.0/ipoim/G42494_03.pdf). Accessed 30 September 2026.
- Oracle, [Retail Demand Forecasting Cloud Service — Get Started](https://docs.oracle.com/en/industries/retail/demand-forecasting/23.2.301.0/). Accessed 30 September 2026.
- Oracle, [Retail Demand Forecasting Methods](https://docs.oracle.com/cd/E12475_01/rdf/pdf/160/html/user_guide/output/fc_methods.htm). Accessed 30 September 2026.

[^1]: Oracle documents seasonality as a forecast parameter estimated from historical demand and used with current sales to generate demand forecasts.
