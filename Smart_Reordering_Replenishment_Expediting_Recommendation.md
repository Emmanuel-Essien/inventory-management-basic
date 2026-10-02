# Replenishment Expediting Recommendation

## Description

Replenishment Expediting Recommendation identifies incoming replenishment orders that may arrive too late to prevent an inventory shortage and recommends reviewing them for possible expedited delivery. The feature connects projected inventory requirements with expected supplier delivery dates so that an existing replenishment order can be acted on before the shortage occurs.

## Purpose

The purpose of this feature is to reduce the risk of stockouts caused by replenishment arriving later than the inventory can support. Instead of creating a completely new order whenever a shortage is projected, the system first checks whether an existing incoming order could be expedited or otherwise adjusted to meet the required date.

## How It Works

1. Monitor items with open replenishment orders or other expected incoming supply.
2. Calculate or obtain the item's projected inventory over the relevant planning period.
3. Identify the date on which projected inventory would fall below the required level if no additional supply arrives.
4. Compare that date with the expected receipt date of the incoming replenishment.
5. If the expected receipt occurs after the projected shortage date, mark the replenishment as potentially late.
6. Determine whether the supplier, order, and purchasing rules allow an expedited-delivery request or other approved action.
7. Generate an expediting recommendation containing the affected order, required date, expected receipt date, and inventory impact.
8. Allow the purchasing or inventory user to review the recommendation and decide whether to expedite, change the order, create alternative supply, or take another approved action.
9. Recalculate the recommendation when demand, inventory, supplier dates, or incoming orders change.

## Information Required

- Item or SKU identifier
- Location
- Current inventory position
- Expected demand
- Reorder point or required inventory level
- Existing replenishment orders
- Ordered quantities
- Expected supplier receipt dates
- Supplier lead time or confirmed delivery date
- Supplier expediting capability or applicable purchasing rules
- Alternative replenishment sources, where available

## Output / Action

- Expediting-risk status for an incoming replenishment order
- Projected shortage date
- Expected receipt date
- Quantity at risk of being unavailable before receipt
- Recommended expediting action
- Affected purchase or replenishment order
- Alert for purchasing or inventory review
- Updated recommendation when supply or demand information changes

## Benefits

- Identifies late replenishment risks before they become actual stockouts.
- Uses existing incoming supply before recommending unnecessary additional purchasing.
- Gives purchasing users a clear reason for an expediting recommendation.
- Connects supplier delivery information with inventory replenishment decisions.
- Can complement supplier lead-time monitoring and stockout-risk monitoring.

## Limitations / Dependencies

- The recommendation depends on accurate demand, inventory, and expected delivery information.
- A supplier may not be able to expedite an order even when a shortage is projected.
- Expediting can increase transportation or supplier costs.
- The feature recommends an action but should not bypass purchasing approval or supplier agreements.
- Alternative replenishment may still be required when an existing order cannot be expedited sufficiently.

## Sources

- Microsoft Learn, [About planning functionality](https://learn.microsoft.com/en-us/dynamics365/business-central/production-about-planning-functionality). Accessed 2 October 2026.
- Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies). Accessed 2 October 2026.
- Microsoft Learn, [Walkthrough: Planning supplies automatically](https://learn.microsoft.com/en-au/dynamics365/business-central/walkthrough-planning-supplies-automatically). Accessed 2 October 2026.
