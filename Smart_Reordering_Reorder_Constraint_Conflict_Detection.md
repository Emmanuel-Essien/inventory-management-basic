# Reorder Constraint Conflict Detection

## Description

Reorder Constraint Conflict Detection is a Smart Reordering feature that identifies conflicts between a replenishment recommendation and the inventory, supplier, or purchasing constraints that govern the item.

The feature does not calculate the reorder point or determine the normal order quantity. Instead, it checks an existing recommendation and identifies conditions that prevent it from being processed normally.

## Purpose

The purpose is to prevent a replenishment recommendation that violates an important inventory or supplier constraint from being treated as a normal order.

The feature provides a clear explanation of the conflict so that the recommendation can be reviewed or corrected before purchasing.

## How It Works

1. Receive a replenishment recommendation from the existing Smart Reordering process.
2. Retrieve the constraints that apply to the item and its replenishment source.
3. Compare the recommended quantity with supplier minimum order quantities and order multiples.
4. Check whether the quantity would exceed the item's configured maximum stock level where applicable.
5. Check whether the expected delivery date satisfies the item's required receipt date.
6. Check whether an approved supplier or other replenishment source can satisfy the recommendation.
7. Identify any missing or contradictory information required to process the recommendation.
8. Create a conflict record containing the affected item, recommendation, conflicting rule, and relevant values.
9. Mark the recommendation for review when a conflict is detected.
10. Recheck the recommendation when the conflicting information or constraint is changed.

## Information Required

- Item or SKU
- Location
- Recommended reorder quantity
- Reorder point
- Maximum stock level
- Supplier minimum order quantity
- Order multiple or case size
- Supplier lead time
- Required receipt date
- Approved suppliers
- Available replenishment sources
- Existing incoming inventory
- Applicable inventory and purchasing constraints

## Output / Action

- Conflict status for the reorder recommendation
- Item affected by the conflict
- Original recommended quantity
- Constraint causing the conflict
- Relevant values used in the conflict check
- Review alert when the recommendation cannot be processed normally
- Updated conflict status when the issue is resolved

## Benefits

- Prevents invalid replenishment recommendations from being processed without review.
- Makes the specific cause of a conflicting recommendation visible.
- Provides a consistent method for handling unusual combinations of inventory and supplier constraints.
- Helps users distinguish between a normal reorder and one requiring an exception or manual decision.
- Creates a record of conflicts that can be reviewed later.

## Limitations / Dependencies

- The feature depends on accurate inventory, supplier, lead-time, and ordering-constraint information.
- Not every detected conflict can be resolved automatically because the correct action may depend on business circumstances.
- Poorly configured constraints can generate unnecessary conflict alerts.
- The feature identifies conflicts but does not replace the existing reorder calculation or purchasing approval process.

## Sources

- Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies). Accessed 30 September 2026.
- Microsoft Learn, [Design details: Planning parameters](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-planning-parameters). Accessed 30 September 2026.