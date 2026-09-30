# Smart Reordering — Reorder Service Level Monitoring

## Objective
Measure the service level actually achieved for each inventory item and identify items whose fulfillment performance remains below the intended target.

## Business Value
Reorder settings should be evaluated against actual fulfillment results. Monitoring service level helps the inventory team identify persistent shortages and investigate whether reorder points, safety stock, replenishment timing, or supplier lead times need review.

## Inputs
- SKU or item identifier
- Units requested
- Units fulfilled
- Shortage or stockout events
- Target service level
- Replenishment order information
- Supplier lead-time information

## Calculation
A unit-fill service level can be calculated as:

\[
Service\ Level=\frac{Units\ Fulfilled}{Units\ Requested}\times100
\]

The feature should also count shortage events so that a high unit-fill percentage does not hide repeated availability problems.

## Expected Output
For each SKU:
- Target service level
- Achieved service level
- Units requested
- Units fulfilled
- Number of shortage events
- Relevant replenishment information
- Review alert when achieved service level remains below target

## Process
1. Collect demand and fulfillment records.
2. Calculate achieved service level for the selected period.
3. Count shortage events.
4. Compare achieved performance with the target.
5. Review replenishment orders and supplier lead times for underperforming items.
6. Flag the item for inventory-policy review.

## Interpretation
A sustained service-level gap can indicate that the current reorder point, safety stock, replenishment timing, or supplier performance is not providing the intended availability. The feature identifies items for review; it does not automatically alter reorder parameters.

## Limitations
Accurate results require reliable demand, fulfillment, cancellation, and stockout records. The organization should use a consistent service-level definition when comparing performance across periods.

## Source
Oracle Supply Chain documentation:
https://docs.oracle.com/en/cloud/saas/supply-chain-and-manufacturing/25d/faupc/service-level.html
