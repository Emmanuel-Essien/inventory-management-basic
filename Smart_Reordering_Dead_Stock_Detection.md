# Dead Stock Detection

## Description

Dead Stock Detection is a Smart Reordering feature that identifies inventory that is no longer moving, or is moving so slowly that continuing to replenish it may be wasteful. The feature uses inventory age and movement measures to flag items that may be slow-moving, non-moving, or obsolete before another automatic reorder is created. Oracle describes inventory aging analysis using measures such as inventory turns, weighted average inventory age, and sales percentage.[^1]

## Purpose

The purpose is to prevent the Smart Reordering system from repeatedly ordering products that have little or no current demand. Instead of treating every low-stock item as a reason to reorder, the system checks whether the item is actually moving and whether there is evidence of future demand.

## How It Works

1. Review recent inventory movement, sales or usage, and the age of stock on hand.
2. Calculate indicators such as inventory turns, average inventory age, and the percentage of stock sold over a selected period.[^1]
3. Compare the indicators with configurable thresholds for slow-moving and dead stock.
4. When an item meets the configured dead-stock conditions, flag it for review.
5. Before creating an automatic reorder, check the item's dead-stock status. The system can pause or suppress the normal reorder recommendation unless a valid demand or business rule overrides the check.
6. Recommend an appropriate follow-up action, such as holding the reorder, transferring stock to another location with demand, reviewing a promotion, or considering disposal for genuinely obsolete stock.[^1]
7. Keep slow-moving stock separate from confirmed obsolescence because low recent usage does not automatically mean an item has no future use.[^2]

## Information Required

- Item or SKU
- Current stock quantity
- Inventory age or receipt dates
- Recent sales or usage history
- Inventory turns
- Average inventory age
- Sales percentage or movement rate
- Configurable inactivity or slow-moving thresholds
- Known future demand, reservations, or critical-use requirements
- Location information, where inventory can be transferred

## Output / Action

- Dead-stock or slow-moving status for an item
- A warning before an automatic reorder is created
- A recommended action such as hold reorder, transfer, promotion review, or obsolete-stock review
- An explanation showing the movement and ageing indicators that triggered the alert

## Benefits

- Reduces unnecessary replenishment of items with little or no movement.
- Helps lower storage and carrying costs.
- Makes ageing inventory visible before it becomes a larger financial problem.
- Can redirect usable stock to locations where there is demand instead of buying more inventory.[^1]

## Limitations / Dependencies

- Thresholds for dead stock vary by product type, industry, and business policy.
- Slow-moving does not always mean obsolete; critical spare parts or seasonal items may have low recent movement but still be important.[^2]
- The feature depends on accurate transaction history, stock dates, and future-demand information.
- Suppressing a reorder without checking valid demand could cause a stockout for an item that is intentionally slow-moving but still required.

## Sources

- Oracle, [AI Agent: Inventory Aging Advisor](https://docs.oracle.com/en/cloud/saas/readiness/scm/26a/inv26a/26A-inventory-wn-f41414.htm). Accessed 7 October 2026.
- IBM Community, [Lets talk about why we talk about obsolete inventory so much](https://community.ibm.com/community/user/blogs/dylan-jones/2026/04/19/lets-talk-about-why-we-talk-about-obsolete-invento). Accessed 7 October 2026.

[^1]: Oracle, [AI Agent: Inventory Aging Advisor](https://docs.oracle.com/en/cloud/saas/readiness/scm/26a/inv26a/26A-inventory-wn-f41414.htm). Accessed 7 October 2026.
[^2]: IBM Community, [Lets talk about why we talk about obsolete inventory so much](https://community.ibm.com/community/user/blogs/dylan-jones/2026/04/19/lets-talk-about-why-we-talk-about-obsolete-invento). Accessed 7 October 2026.
