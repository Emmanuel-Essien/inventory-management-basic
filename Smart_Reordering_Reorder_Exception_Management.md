# Reorder Exception Management

## Description

Reorder Exception Management is a Smart Reordering feature that identifies replenishment recommendations that cannot be processed normally because of conflicting inventory rules, supplier constraints, missing information, or timing problems.

Instead of silently producing an unsuitable reorder recommendation, the feature records the exception and provides the information needed for review.

## Purpose

The purpose is to prevent invalid or impractical reorder recommendations from moving directly into the purchasing process.

Normal Smart Reordering features can calculate when and how much to reorder, but unusual conditions may prevent those recommendations from being safely executed. This feature provides a controlled way to identify and handle those conditions.

## How It Works

1. Receive a replenishment recommendation from the existing reordering process.
2. Check the recommendation against the item's inventory and ordering constraints.
3. Detect conditions that prevent normal processing, such as a quantity below the supplier minimum order quantity, an invalid order multiple, insufficient lead time, or missing required data.
4. Create an exception record containing the item, recommendation, and reason for the exception.
5. Assign the exception a status such as pending review, resolved, or rejected.
6. Notify the appropriate user or team when an exception requires action.
7. Allow the recommendation to be corrected, approved with an override, or rejected according to the business rules.
8. Record the final resolution for later review and auditing.
9. Re-evaluate the recommendation when the information causing the exception changes.

## Information Required

- Item or SKU
- Location
- Recommended reorder quantity
- Reorder point
- Current inventory position
- Maximum stock level
- Supplier information
- Supplier minimum order quantity
- Order multiple or case size
- Supplier lead time
- Expected delivery date
- Existing incoming orders
- Exception rules and thresholds

## Output / Action

- Exception status
- Item affected by the exception
- Original reorder recommendation
- Reason for the exception
- Information causing the conflict
- Required review or corrective action
- Record of the final resolution

## Benefits

- Prevents unsuitable reorder recommendations from being processed without review.
- Makes unusual inventory and supplier conditions visible to users.
- Provides a consistent method for handling exceptions.
- Creates a record of why a reorder recommendation was changed, approved, or rejected.

## Limitations / Dependencies

- The feature depends on accurate inventory, supplier, lead-time, and ordering-constraint information.
- Exception rules must be defined clearly to avoid excessive or unnecessary alerts.
- Some exceptions require a human decision because the system may not have enough information to determine the appropriate business action.
- Resolving an exception does not guarantee that the supplier or inventory conditions will remain unchanged.
- The feature should complement existing reordering calculations rather than replace them.

## Sources

- Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies). Accessed 30 September 2026.
- Microsoft Learn, [Design details: Planning parameters](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-planning-parameters). Accessed 30 September 2026.