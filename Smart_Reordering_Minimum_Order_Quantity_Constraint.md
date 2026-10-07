# Minimum Order Quantity Constraint

## Description

Minimum Order Quantity Constraint is a Smart Reordering feature that makes sure a recommended purchase quantity is not smaller than the minimum quantity accepted by the supplier. If the calculated reorder quantity is below the supplier's minimum, the system raises it to the minimum order quantity instead of creating an order that the supplier cannot fulfill. Microsoft Business Central documents this type of order modifier as increasing a suggested order to the specified minimum order quantity.[^1]

## Purpose

The purpose is to make reorder recommendations practical and supplier-compliant. The feature prevents the Smart Reordering process from generating purchase orders that are too small to meet a supplier's minimum requirement.

## How It Works

1. Receive the normal reorder quantity calculated from inventory demand and the item's reordering policy.
2. Check the supplier's minimum order quantity for the item.
3. If the recommended quantity is below the minimum, increase it to the minimum order quantity.[^1]
4. Check other constraints such as the maximum order quantity, order multiple, storage limit, and available budget.
5. If two constraints conflict, flag the recommendation for review instead of silently creating an invalid order.
6. Present the final quantity and explain when the quantity was increased because of the supplier's minimum requirement.

## Information Required

- Item or SKU
- Supplier
- Normal recommended reorder quantity
- Supplier minimum order quantity
- Maximum order quantity, if applicable
- Order multiple or pack size, if applicable
- Maximum inventory or storage limit
- Unit purchase cost
- Available purchasing budget, where relevant

## Output / Action

- A supplier-compliant reorder quantity
- An explanation when the quantity is increased to meet the minimum order quantity
- A warning when the minimum order quantity conflicts with storage, budget, or maximum-order constraints
- A recommendation for manual review when constraints cannot all be satisfied

## Benefits

- Prevents orders that are below the supplier's minimum requirement.
- Reduces the need for manual correction of small or invalid purchase orders.
- Makes the Smart Reordering recommendation more realistic and actionable.
- Helps the system consider supplier ordering rules when determining replenishment quantities.

## Limitations / Dependencies

- Supplier minimum quantities must be accurate and kept up to date.
- Increasing an order to the supplier minimum can create excess inventory or higher carrying costs.
- The feature must be coordinated with maximum order quantity, order multiples, storage limits, and budget constraints.
- A minimum order quantity by itself does not determine whether an item actually needs replenishment; it only modifies the quantity after a reorder need has been identified.

## Sources

- Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies). Accessed 7 October 2026.
- Microsoft Learn, [Design details: Planning parameters](https://learn.microsoft.com/en-gb/dynamics365/business-central/design-details-planning-parameters). Accessed 7 October 2026.

[^1]: Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies). Accessed 7 October 2026.
