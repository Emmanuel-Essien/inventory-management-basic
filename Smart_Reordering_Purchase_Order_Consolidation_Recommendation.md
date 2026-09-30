# Purchase Order Consolidation Recommendation

## Description

Purchase Order Consolidation Recommendation is a Smart Reordering feature that identifies compatible replenishment requirements and recommends grouping them into fewer purchase orders. The feature can consolidate eligible requirements that share conditions such as supplier, business unit, buyer, item, or other configured purchasing attributes.

Oracle procurement documentation describes consolidating requisition lines into purchase orders when specified grouping conditions are shared.[^1][^2]

## Purpose

The purpose is to reduce unnecessary purchase-order fragmentation when multiple replenishment requirements can be handled together. Instead of creating separate purchase orders for every eligible replenishment requirement, the system can identify groups that may be combined while preserving requirements that cannot safely be consolidated.

## How It Works

1. Collect open replenishment requirements that are ready for purchasing.
2. Group requirements by configured consolidation attributes, such as supplier, purchasing unit, buyer, currency, and location.
3. Check that the requirements are compatible for consolidation.
4. Identify requirements that would create separate purchase orders because their supplier, dates, units of measure, or other required attributes differ.
5. Calculate the combined quantity and estimated purchase value for each eligible group.
6. Generate a consolidation recommendation rather than automatically changing the approved purchasing data.
7. Allow the purchasing user to review, accept, reject, or modify the recommendation.
8. Create or update purchase orders according to the approved grouping rules.

## Information Required

- Replenishment requirements
- Item or SKU
- Required quantity
- Supplier
- Supplier site, where applicable
- Business unit or purchasing organization
- Buyer
- Currency
- Unit of measure
- Requested or required delivery date
- Ship-to location
- Existing purchase orders and open purchase-order lines
- Configured consolidation rules

## Output / Action

- Recommended groups of replenishment requirements
- Proposed combined quantities
- Estimated purchase value for each group
- Requirements that cannot be consolidated and the applicable reason
- Suggested purchase-order grouping for purchasing review
- Optional creation or update of consolidated purchase orders after approval

## Benefits

- Can reduce the number of purchase orders sent to the same supplier.
- Makes compatible replenishment requirements easier to manage together.
- Can reduce duplicate purchasing administration.
- Provides purchasing users with a clear explanation of why requirements were or were not grouped.
- Can complement Supplier Selection Recommendation and Replenishment Quantity Recommendation features.

## Limitations / Dependencies

- Requirements cannot always be consolidated because suppliers, locations, dates, currencies, units of measure, or other purchasing conditions may differ.
- Consolidation rules must match the organization's procurement policies.
- Combining orders can affect delivery schedules and should not override item-specific requirements.
- The feature depends on accurate supplier, item, quantity, and purchasing data.
- Recommendations should be reviewed before purchase orders are finalized when approval controls are required.

## Sources

- Oracle, [Purchase Order Consolidation](https://docs.oracle.com/en/applications/peoplesoft/financials-and-supply-chain-management/9.2.056/peoplesoft-purchasing/purchase-order-consolidation.html). Accessed 30 September 2026.
- Oracle, [Group Requisitions Options](https://docs.oracle.com/en/cloud/saas/procurement/26b/oapro/group-requisitions-options.html). Accessed 30 September 2026.
- Oracle, [Creating Purchase Orders](https://docs.oracle.com/cd/E16582_01/doc.91/e15140/creating_purchase_orders.htm). Accessed 30 September 2026.

[^1]: Oracle documents grouping requisition lines into a single purchase order when configured attributes match.
[^2]: Oracle documents purchase-order consolidation by supplier and other purchasing attributes.
