# Order Quantity Optimization (Economic Order Quantity)

## Description

Order Quantity Optimization determines the order quantity that minimizes the combined annual cost of placing orders and holding stock for an item, using the Economic Order Quantity (EOQ) model. EOQ balances two costs that move in opposite directions as order size changes: ordering cost falls as orders get larger and less frequent, while holding cost rises as more average stock sits on the shelf.[^1] This is a different objective from the ceiling-fill rule in Replenishment Quantity Recommendation, which sizes an order to the physical storage maximum without reference to cost.

## Purpose

Replenishment Quantity Recommendation answers "how much fits." This feature answers "how much is cheapest," and reconciles the two whenever they disagree, so the final recommendation is never more expensive than it needs to be.

## How It Works

1. Compute annual demand, `D = d × 365`, using `d` from Demand Forecasting. No separate demand tracking is needed here; this feature only converts a daily figure to an annual one.
2. Compute holding cost per unit per year, `H = C × I`, where `C` is the item's unit cost and `I` is a holding rate.
3. Compute the unconstrained cost-optimal quantity: `Q* = √(2DS / H)`, where `S` is the ordering cost.[^2] At this quantity, annual ordering cost and annual holding cost come out equal; this is a useful check on the arithmetic.[^1]
4. Round `Q*` to whichever of the two neighboring whole-case quantities gives the lower total cost, `TC(Q) = (D/Q) × S + (Q/2) × H`, comparing both directly rather than always rounding the same way. This gives `Q_EOQ`.
5. Compare `Q_EOQ` against `Q_ceiling`, the largest whole-case quantity Replenishment Quantity Recommendation would allow without exceeding the item's maximum stock level. Because `TC(Q)` decreases for every `Q` below `Q*`, whenever `Q_ceiling` is smaller than `Q_EOQ`, `Q_ceiling` is itself already the cheapest quantity that fits, and is used directly, with no further cost calculation.
6. Otherwise, `Q_EOQ` is used, since it costs less than filling to the ceiling would.
7. Nothing here is stored long-term: because `D` shifts whenever `d` does, `Q*` is recomputed fresh at each stock-arrival cycle, the same cadence already used by the other Smart Reordering features.
8. The reconciled quantity is passed into the same recommend-then-approve flow already used by Replenishment Quantity Recommendation; this feature refines that quantity rather than replacing how it is presented for approval.

## Information Required

- Item, and location or SKU where relevant
- `d`, from Demand Forecasting, used to derive `D`
- `S`, ordering cost: one value for the whole system, entered by a person
- `C`, unit cost per item (source to be specified, likely Vendor Relations)
- `I`, holding rate per item, entered by a person
- Case size, shared with Replenishment Quantity Recommendation
- `Q_ceiling`, the ceiling-constrained maximum quantity, from Replenishment Quantity Recommendation

## Output / Action

- The cost-optimal order quantity, rounded to whole cases
- The final reconciled quantity: whichever of `Q_EOQ` and `Q_ceiling` is smaller
- The reconciled quantity, passed into the same approval and purchasing flow as Replenishment Quantity Recommendation

## Benefits

- Minimizes ordering and holding cost rather than defaulting to filling the shelf.
- Automatically defers to the storage ceiling when the ceiling is the binding constraint, without a separate rule to maintain.
- Neither case-rounding direction is fixed in advance; both whole-case neighbors of `Q*` are compared directly.
- Recomputes automatically as demand shifts, since `D` inherits from the already-automatic `d`.

## Limitations / Dependencies

- Depends on `C` from another module (source to be specified); `H` cannot be computed without it.
- `S` and `I` are manually entered and can go stale: `I` if storage or capital costs change for an item, `S` if the ordering process itself changes. Because `S` is shared across the whole system, a stale value affects every item's calculation at once, not just one.
- The standard EOQ model assumes steady demand and does not cover a shortfall. That case remains entirely with Replenishment Quantity Recommendation's emergency-order path and is unaffected by this feature.

[^1]: Zoho Inventory, [Economic Order Quantity (EOQ): formula, calculator, and worked example](https://www.zoho.com/inventory/academy/inventory-management/economic-order-quantity.html). Accessed 29 September 2026.
[^2]: SRM Institute of Science and Technology, [Economic Order Quantity (lecture slides)](https://webstor.srmist.edu.in/web_assets/srm_mainsite/files/downloads/Economic_order_quantity.pdf). Accessed 29 September 2026.
