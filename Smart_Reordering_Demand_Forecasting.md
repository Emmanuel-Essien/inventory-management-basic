# Demand Forecasting

## Description

Demand Forecasting is a Smart Reordering feature that computes each item's average daily demand, `d`, automatically from that item's own sales history, so `d` is never a manually entered guess and stays current as real demand shifts. The technique used is exponential smoothing, where each new estimate blends today's actual sales with the previous estimate, and the influence of every past day fades gradually rather than dropping out at a fixed cutoff.[^1]

## Purpose

`d` is the direct input to the reorder point calculation, `R = d × L + SS`, in the Reorder Point Monitoring feature. That formula is only as accurate as `d`, so this feature exists to keep `d` true to what the item is actually doing rather than a number someone typed in once and forgot. This mirrors how automatic forecasting is meant to work elsewhere: a baseline forecast is generated from an item's own historical transaction data, not typed in by hand.[^2]

## How It Works

1. Each day, the item's actual sales quantity is recorded (source to be specified, likely Item Identification / Core Storekeeping).
2. `d` is updated using the exponential smoothing formula: **new `d` = `alpha` × today's actual sales + (1 − `alpha`) × previous `d`**.[^1] Unrolling this recursion shows the weight on a sale from `k` days ago is `alpha × (1 − alpha)^k`, a smoothly decaying weight rather than a hard include/exclude cutoff. Because of this, only the current `d` needs to be stored per item; no window of raw daily history needs to be kept or replayed.
3. `alpha` is set per item, not one constant for the whole system, since nothing about an item's storage space indicates how volatile that item's own demand is.
4. `alpha` is recomputed once per stock-arrival cycle, the same event the Replenishment Quantity Recommendation feature already treats as significant. At each arrival, a spread of candidate `alpha` values is tested against the cycle's actual daily sales: for each candidate, the forecast error for every day in the cycle is calculated, squared, and summed (sum of squared errors, SSE), and the candidate with the lowest SSE becomes the item's `alpha` until the next arrival.[^3]
5. For a new item with no completed cycle yet, `d` is seeded from a comparable item already in the system (source of "comparable" to be specified). The seed's influence fades according to `(1 − alpha)^k`, so the item is run at a deliberately high provisional `alpha` at first, since the smaller `alpha` is, the more the initial value matters.[^1] The item switches to its own per-item, SSE-selected `alpha` at its first stock arrival, the same trigger used for every later refresh.
6. The resulting `d` is passed to Reorder Point Monitoring for use in `R = d × L + SS`.

## Information Required

- Item, and location or SKU where stock is managed separately
- Daily actual sales or outflow quantity for the item (source to be specified)
- The item's current `d` and current `alpha`, stored per item
- The date of the item's last stock arrival, shared with the other two Smart Reordering features
- For a new item: the identity of a comparable item to seed from (source to be specified)

## Output / Action

- The current `d` for each item, passed to Reorder Point Monitoring
- An updated `alpha` per item, recomputed once per stock-arrival cycle
- For a new item: a provisional seeded `d` and a deliberately high starting `alpha`, until its first stock arrival

## Benefits

- `d` reflects each item's actual recent behaviour instead of a stale manually entered figure.
- Storage cost per item is minimal: one `d` and one `alpha`, not a retained window of daily history.
- `alpha` adapts to each item's own demand volatility rather than one setting applied to every item alike.
- A new item gets a usable `d` immediately, rather than starting from zero demand.

## Limitations / Dependencies

- Depends on another part of the system actually recording each item's daily sales or outflow (source to be specified).
- Depends on Item Identification's category or grouping data to find a comparable item to seed a new item from (source to be specified).
- Choosing `alpha` by SSE needs at least one completed stock-arrival cycle of real data to test candidates against; before that, the high-`alpha` provisional phase is a necessary compromise, not a substitute for it.
- A cycle with unusually erratic demand, such as a stockout that suppressed real sales or a one-off promotional spike, will bias that cycle's SSE-selected `alpha` until the next cycle's data corrects it.

[^1]: NIST/SEMATECH, [e-Handbook of Statistical Methods: Single Exponential Smoothing](https://itl.nist.gov/div898/handbook/pmc/section4/pmc431.htm). Accessed 29 September 2026.
[^2]: Microsoft Learn, [Guide: Create a baseline forecast](https://learn.microsoft.com/en-us/dynamics365/supply-chain/master-planning/tasks/create-baseline-forecast) (Supply Chain Management). Accessed 29 September 2026.
[^3]: University of New Mexico, Stat 581, [Exponential Smoothing (ETS) slides, after Hyndman & Athanasopoulos](https://math.unm.edu/~lil/Stat581/8-ets.pdf). Accessed 29 September 2026.
