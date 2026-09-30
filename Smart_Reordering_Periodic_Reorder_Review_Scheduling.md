# Periodic Reorder Review Scheduling

## Description

Periodic Reorder Review Scheduling is a Smart Reordering feature that checks selected inventory items at defined review intervals instead of requiring a reorder decision after every individual inventory transaction. At each review point, the system compares the item's stock position with its reorder level and determines whether replenishment should be proposed.[^1][^2]

## Purpose

The purpose is to support inventory processes where staff review stock on a regular schedule, such as daily, weekly, or another defined interval. It provides a predictable review cycle while keeping the existing reorder-point and replenishment-quantity features responsible for the actual reorder decision and quantity.

## How It Works

1. Assign a review interval to each item or item-location combination, such as daily or weekly.
2. Store the item's next scheduled review date.
3. When the review date arrives, calculate the current inventory position using the latest available stock, demand, and incoming-supply information.
4. Compare the inventory position with the item's reorder level.
5. If the reorder condition is met, create a replenishment review event and pass the item to the existing Replenishment Quantity Recommendation feature.
6. If the reorder condition is not met, record that the item was reviewed and schedule its next review.
7. Prevent duplicate review events within the same review cycle.
8. Allow the review interval to be changed when the item's operating conditions require a different checking frequency.

## Information Required

- Item or SKU
- Location, where applicable
- Current inventory position
- Reorder level
- Review interval
- Next review date
- Open replenishment orders
- Demand and supply information required by the reorder calculation

## Output / Action

- Scheduled next-review date for each item
- Review status showing whether replenishment is required
- Replenishment review event when the reorder condition is met
- Audit record showing when the item was reviewed and what inventory position was observed
- Updated review schedule for the next cycle

## Benefits

- Creates a predictable inventory-review routine.
- Can reduce repeated reorder suggestions when a process intentionally checks stock in time buckets.[^1]
- Provides an audit trail of when items were reviewed.
- Separates the timing of inventory review from the existing logic that decides how much to order.

## Limitations / Dependencies

- A long review interval can delay recognition of a stock change. Microsoft notes that a time bucket can allow inventory to remain below the reorder point for the duration of that bucket before a supply order is suggested.[^1]
- The feature depends on accurate inventory, demand, and incoming-order information at review time.
- Items with highly volatile or critical demand may require more frequent reviews than slow-moving items.
- Scheduling reviews does not replace the reorder-point, safety-stock, stockout-risk, or replenishment-quantity calculations already defined in the project.

## Sources

- Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies). Accessed 30 September 2026.
- Microsoft Learn, [Design details: Planning parameters](https://learn.microsoft.com/en-gb/dynamics365/business-central/design-details-planning-parameters). Accessed 30 September 2026.
- Oracle, [Replenishment Parameters](https://docs.oracle.com/en/industries/retail/retail-inventory-planning-optimization-cloud/26.1.101.0/ipodl/ch-Replenishment-Parameters.htm). Accessed 30 September 2026.
