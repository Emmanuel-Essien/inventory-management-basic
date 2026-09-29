# Replenishment Quantity Recommendation

## Description

Replenishment Quantity Recommendation is a Smart Reordering feature that determines how much of an item to order once the Reorder Point Monitoring feature has signalled that replenishment is needed. A min-max inventory policy works on the same principle: a replenishment order raises the inventory position (on-hand stock plus outstanding orders minus backorders) up to a target maximum whenever the position drops to the reorder point or below.[^1] Microsoft's planning system separates the same two decisions, using distinct policies and order modifiers to size the quantity once the reorder point has been crossed.[^2]

## Purpose

Reorder Point Monitoring answers *when*; this feature answers *how much*, turning a replenishment signal into a quantity that respects the item's storage ceiling and the supplier's packaging.

## How It Works

1. Receive the item's status from Reorder Point Monitoring: reorder needed (position between zero and `R`) or shortfall (position below zero).
2. **Reorder needed.** Calculate `Q = M − position`, where `M` is the item's maximum stock level. This is the order-up-to-maximum rule.[^1] Round `Q` down to the nearest whole case. Rounding down, rather than up, is a deliberate choice: exceeding `M` is a hard limit that can physically overflow the storage space, while ordering slightly early because of a smaller quantity is a soft cost. Microsoft's own order modifiers can push a suggested quantity above the maximum inventory level despite the Maximum Qty. policy,[^2] which is the outcome this rounding rule is designed to avoid.
3. If rounding down gives zero whole cases, do not silently skip the item. Raise an alert naming the item, how far one case would exceed `M`, and the days until stockout calculated from on-hand stock and demand, so a person can choose to accept the overshoot, hold the order, or revise the item's settings.
4. **Shortfall.** Calculate `Q` as at least the size of the shortfall (the amount by which position is below zero), then round `Q` up to the nearest whole case, since the storage ceiling is not the binding constraint once a shortfall exists. Microsoft's planning system takes the same approach for negative projected inventory, suggesting an order sized to the exact deficiency and ignoring the maximum inventory level, reorder quantity, and other order modifiers.[^2]
5. For a shortfall caused by demand already promised to a customer, compare the order's expected delivery date with the date the demand is due. If delivery would be late, the alert states how many days late and how much of the promised quantity can still ship on time, since no quantity rule can close a timing gap.
6. An emergency order sized only to the shortfall may leave the item's position still below `R`. Reorder Point Monitoring evaluates the new position separately and, if it remains below `R`, raises its own reorder-needed signal, which this feature answers with a normal order-up-to-maximum recommendation. The two recommendations are not merged.
7. Present the recommendation for approval, or pass it to the purchasing or production process, depending on the replenishment source. Microsoft documents this recommend-then-approve pattern for its own planning system.[^2]

## Information Required

- Item, and location or SKU where stock is managed separately
- Current inventory position
- Reorder point `R` and maximum stock level `M`
- Case size or order multiple, and minimum order quantity, where applicable
- Replenishment lead time and expected delivery date
- For a shortfall: the date the promised demand is due

## Output / Action

- A recommended replenishment quantity, in whole cases
- A label distinguishing a normal top-up order from an emergency order
- An alert when no whole case fits below the maximum, showing the overshoot and the days until stockout
- A lateness notice on an emergency order, showing days late and the quantity that can still ship on time

## Benefits

- Uses one rule, not case-by-case judgement, to size every normal order.
- Protects the storage ceiling by default, since overflow is a hard failure and a slightly earlier reorder is not.
- Still recommends a workable quantity during a shortfall, when the priority reverses and covering the shortage matters more than the ceiling.
- Surfaces a blocked or late order to a person with the numbers needed to decide, rather than failing silently.

## Limitations / Dependencies

- The recommendation depends on accurate figures for position, `R`, `M`, case size, and lead time from Reorder Point Monitoring and other modules.
- If `M` minus `R` is smaller than one case, every normal reorder for that item rounds down to zero and triggers the zero-case alert. Checking for this at setup, when `R`, `M`, or the case size are entered, would catch it before the item ever reaches its reorder point.
- The lateness check on an emergency order depends on having an accurate promised-demand due date, which this feature does not itself collect.

[^1]: Project Production Institute, [Min / Max Inventory (glossary)](https://projectproduction.org/glossary/min-max-inventory/). Accessed 28 September 2026.
[^2]: Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies) (Business Central). Accessed 28 September 2026.
