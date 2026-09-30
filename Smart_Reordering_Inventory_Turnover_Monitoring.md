# Inventory Turnover Monitoring

## Description

Inventory Turnover Monitoring is a Smart Reordering feature that measures how quickly an item is sold or consumed and how long inventory remains in stock. It helps identify items that are moving quickly, moving slowly, or remaining unused.

## Purpose

The purpose is to give the reordering process a view of inventory movement. Reordering a slow-moving item can tie up storage space and money, while failing to recognize a fast-moving item can increase the risk of stockouts.

## How It Works

1. Collect sales or consumption quantities and inventory values for each item.
2. Calculate the item's turnover over a selected period by comparing usage with the average inventory held during that period.
3. Calculate or display the average number of days inventory remains before being sold or consumed.
4. Compare the current turnover with a defined target or with the item's previous periods.
5. Flag items with unusually low turnover for review before another replenishment order is created.
6. Flag items with unusually high turnover so their reorder settings can be reviewed.
7. Provide the results to the reordering process as supporting information rather than replacing the reorder-point calculation.

## Information Required

- Item and location or SKU
- Historical sales or consumption quantities
- Inventory levels over the selected period
- Selected measurement period
- Current reorder point and maximum stock level
- Optional target turnover or expected days of inventory

## Output / Action

- Inventory turnover measure for each item
- Estimated days inventory remains in stock
- Alert for unusually slow-moving items
- Alert for unusually fast-moving items
- A review signal when reorder settings may no longer match the item's movement

## Benefits

- Helps reduce unnecessary replenishment of slow-moving stock.
- Makes unusually fast or slow inventory movement visible.
- Provides another measure for reviewing reorder settings.
- Can help identify items that consume storage space for long periods.

## Limitations / Dependencies

- Turnover can be misleading when demand is seasonal or irregular.
- Accurate results depend on reliable sales, consumption, and inventory records.
- New items may not have enough history for a useful comparison.
- A low turnover rate does not automatically mean an item should never be reordered because some items may be required despite low demand.
- The feature should support, rather than replace, the main reorder rules.

## Sources

- Microsoft Learn, [Design details: Planning with or without forecast](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-planning-with-or-without-forecast). Accessed 30 September 2026.
- Oracle, [Inventory Turnover](https://docs.oracle.com/en/cloud/saas/supply-chain-and-manufacturing/). Accessed 30 September 2026.
