# Reservation-Aware Reordering

## Description

Reservation-Aware Reordering adjusts the inventory quantity used for replenishment decisions by accounting for stock that has already been reserved or allocated to specific demand. Instead of treating all on-hand stock as freely available, the feature distinguishes usable inventory from inventory committed to existing orders or other requirements.

## Purpose

The purpose of Reservation-Aware Reordering is to prevent the reordering process from assuming that reserved stock can satisfy new demand. This produces a more realistic available-inventory position and helps the system identify replenishment needs before committed stock is consumed.

## How It Works

1. Identify the item and location being evaluated for replenishment.
2. Retrieve the item's current on-hand inventory.
3. Retrieve inventory reservations or allocations associated with existing demand.
4. Identify other relevant supply, such as open purchase orders or inbound transfers, according to the system's planning rules.
5. Calculate the quantity available for new demand by subtracting applicable reserved or allocated quantities from the usable inventory position.
6. Compare the resulting available position with the item's reorder point, minimum level, or other configured replenishment rule.
7. If the available position is below the applicable threshold, pass the net quantity to the existing reordering process.
8. Update the calculation when reservations, demand, receipts, or inventory quantities change.

## Information Required

- Item or SKU identifier
- Location or warehouse
- Current on-hand quantity
- Reserved or allocated quantity
- Open demand or sales-order information
- Expected incoming supply
- Reorder point or minimum inventory level
- Inventory availability and reservation rules

## Output / Action

- Reservation-adjusted available inventory
- Quantity reserved or allocated against existing demand
- Net inventory position used for reordering
- Replenishment-needed status
- Reorder recommendation or alert when the adjusted position falls below the applicable threshold
- Explanation showing how reservations affected the replenishment calculation

## Benefits

- Prevents reserved inventory from being incorrectly treated as freely available stock.
- Produces a more accurate inventory position for replenishment decisions.
- Helps reduce the risk of discovering a shortage only after existing orders consume committed stock.
- Makes the effect of reservations visible to inventory planners.
- Can work alongside existing reorder-point, stockout-risk, and replenishment-quantity features.

## Limitations / Dependencies

- The feature depends on accurate reservation and allocation records.
- Organizations may use different rules for which reservations or demands should be included in availability calculations.
- Incoming supply should only be counted when it satisfies the planning system's timing and eligibility rules.
- The feature adjusts the inventory position used by reordering; it does not replace the organization's existing reorder policy.
- Incorrect reservation data can cause unnecessary replenishment recommendations.

## Sources

- Microsoft Learn, [Priority-based planning](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/planning-optimization/priority-based-planning). Accessed 2 October 2026.
- Microsoft Learn, [Demand-driven planning](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/planning-optimization/ddmrp-planning). Accessed 2 October 2026.
- Oracle, [Netting Supply and Demand in Supply Chain Planning](https://docs.oracle.com/cd/A60725_05/html/comnls/us/mrp/mrsmrp10.htm). Accessed 2 October 2026.
