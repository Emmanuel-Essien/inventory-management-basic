# Expiry-Aware Reordering

## Description

Expiry-Aware Reordering is a Smart Reordering feature for items with limited shelf life. It considers expiration dates of existing inventory and incoming supply before recommending new replenishment.

For limited-shelf-life products, Microsoft Dynamics 365 Supply Chain Management uses expiration dates and First-Expired-First-Out (FEFO) planning so that supply approaching expiration is considered before supply with later expiration dates.[^1]

## Purpose

The purpose is to prevent the system from ordering stock that is likely to expire before it can be sold or consumed.

Normal reorder calculations may treat all available units as equally usable. For perishable or short-life items, that assumption can produce unnecessary replenishment while existing stock is approaching expiry. This feature adds expiry information to the replenishment decision.

## How It Works

1. Identify items configured as having a limited shelf life.
2. Retrieve the quantity, lot or batch, and expiration date of existing inventory.
3. Retrieve the expiration dates and expected receipt dates of relevant incoming supply.
4. Retrieve expected demand and the dates when the inventory will be required.
5. Determine which existing and incoming quantities remain usable for each demand date.
6. Apply a FEFO ordering of usable supply, prioritizing inventory with the earliest expiration date.
7. Compare usable supply with expected demand rather than treating all physical stock as equally available.
8. Identify quantities that may expire before they can be used.
9. Pass the usable inventory position into the existing reorder-point and replenishment calculations.
10. Delay, reduce, or suppress a replenishment recommendation when existing usable supply is sufficient.
11. Raise an expiry-risk alert when inventory is approaching its expiration or required sellable-life limit.
12. Continue to allow normal replenishment when usable inventory cannot cover future demand.

## Information Required

- Item or SKU
- Location
- Current inventory quantity
- Lot or batch identifier
- Manufacturing date, where required
- Expiration date
- Expected demand and demand dates
- Existing purchase or transfer orders
- Expected receipt dates
- Supplier lead time
- Shelf-life period
- Minimum required sellable days, where applicable

## Output / Action

- Usable inventory by demand date
- Items or batches approaching expiration
- Expiry-risk alert
- Quantity expected to expire before use
- Reorder recommendation adjusted for usable inventory
- FEFO allocation sequence
- Review signal when shelf-life constraints prevent normal replenishment

## Benefits

- Reduces the chance of replenishing stock while usable inventory is already sufficient.
- Helps reduce losses from expired inventory.
- Makes expiration risk visible before it becomes an operational problem.
- Improves reorder decisions for food, medicine, cosmetics, and other limited-shelf-life products.
- Works alongside existing reorder-point and replenishment-quantity features instead of replacing them.

## Limitations / Dependencies

- The feature requires reliable lot or batch tracking and accurate expiration dates.
- It is mainly applicable to products with limited shelf life.
- Expected demand must be reasonably accurate to determine whether stock will be used before expiration.
- Different products may have different sellable-life requirements.
- FEFO improves stock allocation but does not guarantee that inventory will be sold before expiration.
- Shelf-life rules can make replenishment planning more complex when existing and incoming supplies have different expiration dates.

## Sources

- Microsoft Learn, [Master planning for products with limited shelf life](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/planning-optimization/shelf-life). Accessed 30 September 2026.
- Microsoft Learn, [How to enable picking by FEFO](https://learn.microsoft.com/en-us/dynamics365/business-central/warehouse-picking-by-fefo). Accessed 30 September 2026.
- Microsoft Learn, [Design details: Warehouse management](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-warehouse-management). Accessed 30 September 2026.

[^1]: Microsoft documents shelf-life-aware master planning that considers expiration dates and attempts to use supply closest to expiration before later-expiring supply.
