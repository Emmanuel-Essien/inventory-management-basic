# Supplier Reliability Scoring

## Description

Supplier Reliability Scoring is a Smart Reordering feature that measures how consistently a supplier meets its expected delivery commitments. Instead of considering only the supplier's nominal lead time, the feature builds a reliability record from historical purchase orders and actual supplier performance.

Supplier reliability can be evaluated using delivery-time and other supplier-performance measures. IBM's supply-chain analytics material identifies supplier reliability and delivery consistency as measurable performance factors, while its documentation describes purchase-order commitment timeliness as the percentage of purchase orders committed on time.[^1][^2]

## Purpose

The purpose is to give the Smart Reordering system a historical measure of supplier delivery reliability that can be shown alongside the supplier's normal lead time.

A supplier with a stated lead time of five days but a history of regularly arriving later should not be represented as having the same delivery risk as a supplier that consistently meets its five-day commitment. The score therefore provides additional information for reorder planning and supplier review.

## How It Works

1. Record each purchase order's promised delivery date and actual receipt date.
2. Calculate the delivery variance for each completed purchase order by comparing the actual receipt date with the promised date.
3. Determine whether each order was delivered on time according to the configured tolerance.
4. Calculate a reliability measure over a defined historical period, such as the percentage of orders delivered on time.
5. Calculate supporting statistics such as average delivery delay and the variation in delivery delay.
6. Give greater weight to recent orders when the system is configured to make the score responsive to recent supplier performance.
7. Store the resulting reliability score and supporting measures for each supplier-item relationship where sufficient history exists.
8. Display the score when a replenishment recommendation is being reviewed.
9. If the reliability score falls below a configured threshold, raise a supplier-performance warning for review.
10. Keep supplier reliability separate from the supplier's contractual lead time so that the system does not silently replace the maintained purchasing value.

## Information Required

- Supplier
- Item or SKU
- Purchase order number
- Purchase order date
- Promised delivery date
- Actual receipt date
- Quantity ordered and received, where relevant
- Configured on-time delivery tolerance
- Historical period used for scoring
- Minimum number of completed orders required for a score
- Optional supplier-item location relationship

## Output / Action

- Supplier reliability score
- Percentage of orders delivered on time
- Average delivery delay
- Delivery-delay variability
- Number of completed orders used in the calculation
- Supplier-performance warning when configured conditions are met
- Reliability information displayed alongside supplier selection or reorder recommendations

## Benefits

- Makes supplier delivery performance measurable instead of relying only on the stated lead time.
- Gives purchasing and inventory users a historical view of delivery consistency.
- Can expose suppliers whose recent performance differs from their expected lead time.
- Provides useful supporting information for reorder and supplier-review decisions.
- Can complement the existing Supplier Lead Time Monitoring and Supplier Selection Recommendation features.

## Limitations / Dependencies

- The score is only as reliable as the purchase-order and receipt dates recorded by the system.
- A supplier with very few completed orders may not have enough history for a meaningful score.
- Delivery delays caused by factors outside the supplier's control may require separate interpretation.
- A historical score does not guarantee future supplier performance.
- Different items, locations, order sizes, or shipping methods can have different delivery performance, so supplier-wide scores may hide important differences.
- The score should inform the reordering process rather than automatically changing contractual lead-time values.

## Sources

- IBM, [Supply Chain — IBM SPSS Statistics](https://www.ibm.com/products/spss-statistics/supply-chain). Accessed 30 September 2026.
- IBM, [PO Commit Timeliness](https://www.ibm.com/support/pages/po-commit-timeliness). Accessed 30 September 2026.
- IBM Research, [Product hardware complexity and its impact on inventory and customer on-time delivery](https://research.ibm.com/publications/product-hardware-complexity-and-its-impact-on-inventory-and-customer-on-time-delivery). Accessed 30 September 2026.

[^1]: IBM describes ANOVA and regression analysis as ways to assess supplier reliability, delivery times, and quality metrics.
[^2]: IBM defines a purchase-order commitment timeliness KPI using the proportion of purchase orders committed on time.
