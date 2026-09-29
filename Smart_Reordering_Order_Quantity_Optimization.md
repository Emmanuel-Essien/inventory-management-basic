# Order Quantity Optimization

## Description

Order Quantity Optimization is a Smart Reordering feature that calculates the most cost-effective batch size for a replenishment order. While the Replenishment Quantity Recommendation feature uses physical constraints to set a hard ceiling (`M`), this feature applies the Economic Order Quantity (EOQ) model to find a target size that minimizes the combined annual costs of placing orders and holding inventory.[^1] The two features run in parallel, and their results are mathematically reconciled before an order is placed.

## Purpose

The purpose is to answer *what is the cheapest order size?* Every order placed incurs a fixed administrative or delivery cost, which favours ordering in large batches. However, holding stock incurs capital lock-up and storage costs, which favours ordering in small batches. This feature finds the exact quantity where these two opposing costs are balanced, avoiding both excessive ordering overhead and unnecessarily high stockholding.

## How It Works

1. Receive the item's average daily demand `d` from Demand Forecasting. Calculate annual demand as `D = d × 365`.
2. Compute the theoretical optimal quantity: `Q_EOQ = √(2 × D × S / (C × i))`. Here, `S` is the fixed cost per order, `C` is the unit purchase cost, and `i` is the annual holding rate percentage (so `C × i` represents the annual holding cost per unit, `H`).[^1]
3. **Case-size rounding:** `Q_EOQ` rarely lands on a whole case. Calculate the total annual cost for the nearest whole-case multiples above and below `Q_EOQ` using the formula `TC(Q) = (D / Q) × S + (Q / 2) × (C × i)`. Select the case quantity that yields the lower total cost.
4. **Ceiling reconciliation:** Compare the cost-optimal case quantity against the physical ceiling limit (`Q_ceiling = M - position`) calculated by the Replenishment Quantity Recommendation feature.
5. If `Q_ceiling < Q_EOQ`, the ceiling restricts the order. Because the total cost curve `TC(Q)` strictly decreases as it approaches `Q_EOQ` from the left, the cheapest *feasible* choice is simply `Q_ceiling`. The system recommends `Q_ceiling`.[^2]
6. If `Q_ceiling >= Q_EOQ`, the cost-optimal quantity fits safely on the shelf. The system ignores the physical ceiling's blind fill rule and recommends the smaller, genuinely cheaper `Q_EOQ`.
7. **Shortfall override:** If the item's position is below zero (a shortfall), cost optimization is bypassed entirely. The system defers to the emergency shortfall logic (order at least the deficiency, rounded up to the nearest case) to prioritize service over batch-cost efficiency.
8. **Minimum Order Quantity (MOQ):** If a supplier's MOQ is greater than `Q_EOQ`, the system rounds up to the MOQ (provided it does not exceed `Q_ceiling`).

## Information Required

- Item, and location or SKU where stock is managed separately
- Current inventory position and maximum stock level `M`
- Average daily demand `d` (from Demand Forecasting)
- Case size or order multiple, and supplier MOQ
- Fixed ordering cost `S` and annual holding rate `i` (accounting or policy inputs)
- Unit purchase cost `C` (from vendor catalog or item master)

## Output / Action

- A recommended cost-optimal replenishment quantity, in whole cases, reconciled against physical storage limits
- A system alert triggering human intervention if `MOQ > Q_ceiling` (meaning the smallest order the supplier accepts will physically overflow the shelf)
- A calculation fallback to `Q_ceiling` if `C` or `i` are missing or zero, preventing a division-by-zero error

## Benefits

- Prevents ordering 6 months of stock for an expensive, slow-moving item just because there is physical room for it on the shelf.
- Splitting holding cost into `C × i` dynamically scales the holding penalty as item prices change, requiring no manual updates to `H`.
- Merges seamlessly with physical limits: the system never recommends a quantity that overflows the shelf, but stops short of the ceiling when it is cheaper to do so.
- Case-size rounding is determined by mathematical cost comparison rather than arbitrary round-up/round-down rules.

## Limitations / Dependencies

- Inherits the accuracy of `d` from the Demand Forecasting module; highly volatile demand reduces EOQ effectiveness.
- Relies on accurate accounting inputs for `S` (ordering cost) and `i` (holding rate percentage). If these are set arbitrarily, the resulting quantity will be mathematically optimal but practically incorrect.

[^1]: Harris, F. W., "How Many Parts to Make at Once", *Factory, The Magazine of Management* (1913). Standard EOQ model formulation.
[^2]: Total cost curve behavior establishes that for any constrained quantity `Q < Q_EOQ`, the largest feasible quantity provides the minimum achievable cost.
