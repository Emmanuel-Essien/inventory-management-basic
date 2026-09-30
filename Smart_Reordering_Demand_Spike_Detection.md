# Demand Spike Detection

## Description

Demand Spike Detection is a Smart Reordering feature that identifies unusually large short-term demand for an item compared with the item's normal demand level. It uses a configurable spike threshold to distinguish an unusual order or sales quantity from ordinary demand, so the replenishment process can react before the temporary increase causes an inventory shortage.[^1]

## Purpose

The purpose of Demand Spike Detection is to make Smart Reordering respond to short-term demand changes that may be too sudden to wait for the normal forecasting cycle.

The feature does not replace Demand Forecasting. Demand Forecasting maintains the item's underlying demand estimate, while Demand Spike Detection identifies exceptional demand that should receive separate attention during replenishment planning.

## How It Works

1. Collect the item's recent or upcoming demand transactions.
2. Obtain the item's normal demand level from the existing demand-planning process.
3. Store a configurable order-spike threshold for the item. Microsoft describes an order spike threshold as a minimum quantity that qualifies unusually high daily demand as a spike.[^1]
4. Compare each relevant demand quantity with the threshold.
5. Mark demand that exceeds the threshold as a spike.
6. Calculate the additional quantity represented by the spike so the replenishment process can see how much demand is above the normal level.
7. Recalculate the item's projected inventory using the newly identified demand.
8. If the spike creates a replenishment condition, pass the item to the existing Reorder Point Monitoring and Replenishment Quantity Recommendation features.
9. Record the spike and its effect on the replenishment decision for later review.
10. Remove the spike condition when the demand returns to normal or the planning period containing the spike has passed.

## Information Required

- Item or SKU
- Location, where inventory is managed separately
- Recent or upcoming demand quantities
- Normal demand level or baseline
- Item-specific spike threshold
- Relevant demand dates
- Current inventory position
- Open replenishment orders

## Output / Action

- Spike or normal-demand status for each relevant demand period
- Quantity identified as exceptional demand
- Updated projected inventory after the spike is considered
- Replenishment-review signal when the spike creates a shortage or reorder condition
- Record of the detected spike for later analysis

## Benefits

- Gives the replenishment process an early signal when demand is unusually high.
- Prevents an exceptional order from being treated as ordinary demand without review.
- Allows the threshold to be configured per item because different items can have different demand patterns.[^1]
- Helps the system distinguish a short-term demand event from the item's longer-term demand estimate.

## Limitations / Dependencies

- The threshold must be chosen carefully; a threshold that is too low can create too many spike alerts, while a high threshold can miss meaningful events.
- The feature depends on accurate demand transactions and a usable baseline demand value.
- A detected spike does not explain why demand increased; staff may need to investigate promotions, customer orders, or other business events.
- A spike alert does not by itself determine the final order quantity.
- The feature should work alongside Demand Forecasting rather than replacing it.

## Sources

- Microsoft Learn, [Demand-driven planning](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/planning-optimization/ddmrp-planning). Accessed 30 September 2026.
- Microsoft Learn, [Buffer profile and levels](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/planning-optimization/ddmrp-buffer-profile-and-levels). Accessed 30 September 2026.

[^1]: Microsoft documents an item-level order-spike threshold that identifies demand exceeding normal expectations and can increase the reorder quantity during high-demand periods.
