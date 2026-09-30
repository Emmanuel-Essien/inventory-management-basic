# ABC Inventory Classification for Reordering

## Description

ABC Inventory Classification for Reordering groups inventory items according to their relative annual consumption value. Annual consumption value (ACV) can be calculated as annual usage multiplied by unit cost. Items are then ranked by ACV and assigned to A, B, or C categories using defined cumulative-value thresholds.[^1][^2]

## Purpose

The purpose is to help the Smart Reordering process apply different levels of attention to items according to their financial importance. The feature does not replace reorder-point or quantity calculations; it determines which items should receive tighter monitoring and review.

## How It Works

1. Collect each item's annual usage and unit cost.
2. Calculate annual consumption value: **ACV = Annual Usage × Unit Cost**.[^1]
3. Sort items from highest to lowest ACV.
4. Calculate each item's percentage of total ACV and its cumulative percentage.
5. Assign A, B, or C categories using configurable cumulative-value thresholds. For example, the system may use an A threshold and a B threshold rather than assuming fixed percentages.[^1]
6. Store the classification for each item or item-location combination.
7. Use the classification to set review priority. A items can receive tighter monitoring, while B and C items can use progressively lighter review controls.[^2]
8. Recalculate the classification on a scheduled basis so changes in usage or cost can move an item between categories.

## Information Required

- Item or SKU
- Location, where inventory is managed separately
- Annual usage or historical consumption data
- Unit cost
- A-category cumulative-value threshold
- B-category cumulative-value threshold
- Classification review frequency

## Output / Action

- Annual consumption value for each item
- Percentage and cumulative percentage of total inventory value
- A, B, or C classification
- Reorder-review priority associated with the classification
- Alert when an item's classification changes materially

## Benefits

- Helps focus inventory-control effort on items with greater financial impact.
- Provides a consistent way to segment a large inventory list.
- Can support different review frequencies and controls for different item groups.[^2]
- Makes changes in an item's financial importance visible to the reordering team.

## Limitations / Dependencies

- Classification depends on accurate usage and unit-cost data.
- An item's category can change when demand or cost changes, so classifications should be recalculated periodically.
- ABC classification measures relative value and does not by itself measure stockout risk, demand variability, criticality, or supplier reliability.
- Low-value C items may still be operationally critical, so classification should not be the only input to replenishment decisions.

## Sources

- Oracle, [Inventory Optimization Preferences — ABC Category Preferences](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/article_0702084957.html). Accessed 30 September 2026.
- Oracle, [Overview of ABC Analysis](https://docs.oracle.com/en/cloud/saas/supply-chain-and-manufacturing/26b/faims/overview-of-abc-analysis.html). Accessed 30 September 2026.
- Oracle, [Inventory Segmentation Calculation Process](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/article_0702090533.html). Accessed 30 September 2026.

[^1]: Oracle, [Inventory Optimization Preferences — ABC Category Preferences](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/article_0702084957.html). Accessed 30 September 2026.
[^2]: Oracle, [Overview of ABC Analysis](https://docs.oracle.com/en/cloud/saas/supply-chain-and-manufacturing/26b/faims/overview-of-abc-analysis.html). Accessed 30 September 2026.
