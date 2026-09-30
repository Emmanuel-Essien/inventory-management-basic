# Supplier Selection Recommendation

## Description

Supplier Selection Recommendation is a Smart Reordering feature that identifies the most suitable approved supplier for a replenishment order. It evaluates eligible suppliers using purchasing information such as unit price and lead time, while respecting supplier eligibility and ordering constraints.

Microsoft Dynamics 365 Supply Chain Management supports master planning that can evaluate purchase trade agreements and prioritize either the lowest unit price or minimum lead time when determining the vendor for a planned order.[^1] It also supports sourcing products from multiple vendors under configured supplier policies.[^2]

## Purpose

The purpose of this feature is to ensure that a reorder recommendation is not only the correct quantity, but is also assigned to an appropriate supplier.

Existing Supplier Lead Time Monitoring measures supplier delivery performance, but it does not decide which supplier should receive a new replenishment order. This feature uses available supplier information to make that selection.

## How It Works

1. Receive the item, required replenishment quantity, and required receipt date from the existing reordering process.
2. Retrieve the suppliers approved to supply the item.
3. Remove suppliers that cannot satisfy the item, required quantity, location, or ordering conditions.
4. Retrieve the current supplier information, including unit price and expected lead time.
5. Determine the supplier selection rule configured for the item or purchasing process, such as lowest unit price or shortest lead time.
6. Compare the eligible suppliers using the selected rule.
7. Check that the selected supplier can deliver within the required time.
8. If several suppliers satisfy the rule equally, use a secondary criterion such as shorter lead time or lower price to break the tie.
9. Return the selected supplier together with the reason for the recommendation and the expected delivery information.
10. Send the recommendation into the normal purchase approval or purchase-order process.

## Information Required

- Item or SKU
- Required replenishment quantity
- Required receipt date
- Approved suppliers for the item
- Supplier unit price
- Supplier lead time
- Minimum order quantity, where applicable
- Order multiples or packaging constraints, where applicable
- Supplier availability or purchasing status
- Supplier-item trade agreement information
- Supplier selection rule

## Output / Action

- Recommended supplier
- Expected supplier lead time
- Expected receipt date
- Supplier price used for the recommendation
- Reason for supplier selection
- Alternative eligible suppliers when more than one supplier qualifies
- Review alert when no eligible supplier can satisfy the replenishment requirement

## Benefits

- Connects the reorder recommendation to an actual supplier.
- Allows purchasing rules such as price or lead time to be applied consistently.
- Makes the reason for supplier selection visible to the person approving the order.
- Can use information already maintained for supplier and item relationships.
- Helps prevent a reorder recommendation from being created without a valid source of supply.

## Limitations / Dependencies

- Supplier prices and lead times must be accurate and current.
- The feature depends on an approved-supplier or supplier-item relationship being maintained.
- The cheapest supplier may not provide the earliest delivery, so the selection rule must be defined clearly.
- Minimum order quantities, order multiples, contracts, and supplier allocation policies may restrict the available choices.
- The feature recommends a supplier; it does not replace purchasing approval or contract-management processes.

## Sources

- Microsoft Learn, [Master planning with purchase trade agreements](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/planning-optimization/purchase-trade-agreement). Accessed 30 September 2026.
- Microsoft Learn, [Source products and materials from multiple vendors](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/source-from-multiple-vendors). Accessed 30 September 2026.
- Microsoft Learn, [Create a purchase order](https://learn.microsoft.com/en-us/dynamics365/supply-chain/procurement/tasks/create-purchase-order). Accessed 30 September 2026.

[^1]: Microsoft documents supplier and lead-time selection during master planning and allows the search criterion to prioritize minimum lead time or lowest unit price.
[^2]: Microsoft documents multisource purchasing policies that determine which vendor can be assigned to a planned order.
