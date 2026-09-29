# Reorder Point Monitoring

## Description

Reorder Point Monitoring is a Smart Reordering feature that compares each item's inventory position with a stored reorder point and raises a replenishment signal when the position reaches or falls below it. SAP's reorder point planning works the same way: replenishment starts once stock on hand plus confirmed incoming receipts drops under the reorder point.[^1] This feature decides *when* to reorder; *how much* to order is decided by the Replenishment Quantity Recommendation feature.

## Purpose

The purpose is to reorder early enough that demand during the supplier's lead time is covered before the shelf empties. Microsoft describes a reorder point as the demand expected during lead time, and its planning system proposes a supply order as projected inventory heads below that level.[^2] Doing this automatically replaces manual shelf-watching with a consistent check across every item.

## How It Works

1. Each item has a stored reorder point `R`. Microsoft's planning system also allows these settings per stock-keeping unit, so items held in separate locations or variants can have their own.[^3]
2. `R = d × L + SS`, where `d` is average daily demand, `L` is the supplier's lead time in days, and `SS` is safety stock. SAP uses the same relationship and counts safety stock as part of the reorder level.[^1] Microsoft instead treats the reorder point as demand during lead time[^2] and enters safety stock as a separate quantity.[^3] In our system, safety stock is a fixed number entered manually by a person, who can weigh recent demand against the physical space available to store the item.
3. The feature compares `R` with the item's inventory position, not with stock on hand alone. Inventory position is stock on hand plus quantities on order minus backorders.[^4] In our system, demand already promised to customers for a future date is also subtracted, so a promised order that stock cannot cover appears as a negative position. Using stock on hand alone would raise the signal again every day while an earlier order is still on its way.
4. When the position reaches or falls below `R`, the system raises a replenishment signal. Microsoft's planning system first checks for supply that is already on order or due within the lead time, and suggests a new order only if none covers the need.[^2] Our system likewise raises one signal per shortage, so an order already on its way is never duplicated.
5. How often the check runs is a design choice. Microsoft's time-bucket setting checks the level after each bucket instead of after every transaction, mirroring a manual routine of inspecting stock at regular intervals.[^2]
6. The result is one of three states: above `R` (no action), between zero and `R` (reorder needed), or below zero (shortfall, meaning promised demand exceeds all stock and incoming orders). Microsoft treats projected negative inventory as an emergency and suggests an order for the exact deficiency.[^2] The quantity for each state is set by the Replenishment Quantity Recommendation feature.

## Information Required

- Item, and location or SKU where stock is managed separately
- Stock on hand
- Quantities on order (open replenishment orders)
- Demand already promised to customers for future dates
- Average daily demand (source to be specified once more is known about the rest of the system)
- Supplier lead time
- Safety stock, entered manually, with the date it was last changed

## Output / Action

- The item's status: above `R`, reorder needed, or shortfall
- A replenishment signal passed to the Replenishment Quantity Recommendation feature
- A breakdown on the item screen showing `d × L`, the safety stock, the resulting `R`, and the room left below the item's maximum stock level `M`, so the person can see what the safety stock they entered does to the shelf

## Benefits

- Flags replenishment needs before stock runs out instead of after.
- Counts orders already on the way, so the same shortage does not produce repeated signals.
- Checking per time bucket instead of per transaction reduces the number of order suggestions.[^2]
- Leaves the safety stock decision with a person who can see the actual storage space.

## Limitations / Dependencies

- Microsoft notes that projected inventory must be large enough to cover demand until the new order arrives, with safety stock absorbing demand swings up to a targeted service level.[^2] The feature is therefore only as good as the stock, on-order, promised-demand, and lead-time figures it receives from other parts of the system.
- SAP describes safety stock as the buffer for extra consumption during lead time and for late deliveries.[^1] A delay longer than the buffer covers can still cause a stockout.
- A manually entered safety stock, demand figure, or lead time can go stale. The last-changed date makes old values visible, and `R` must be revisited whenever lead time changes. SAP's automatic variant recalculates these values from consumption history, which is a possible later upgrade.[^1]

[^1]: SAP Learning, [Using Forecast in Reorder Point Planning](https://learning.sap.com/courses/consumption-based-planning-and-forecasting-in-sap-cloud-erp/using-forecast-in-reorder-point-planning). Accessed 28 September 2026.
[^2]: Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies) (Business Central). Accessed 28 September 2026.
[^3]: Microsoft Learn, [Design details: Planning parameters](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-planning-parameters) (Business Central). Accessed 28 September 2026.
[^4]: Bricker, D., University of Iowa, [Reorder Point (lecture slides)](https://user.engineering.uiowa.edu/~dbricker/Lecture_Slides/Reorder_Point.pdf). Accessed 28 September 2026.
