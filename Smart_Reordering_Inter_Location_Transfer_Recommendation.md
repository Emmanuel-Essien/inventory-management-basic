# Inter-Location Transfer Recommendation

## Description

Inter-Location Transfer Recommendation is a Smart Reordering feature that checks whether an item needed at one location can be supplied by moving available stock from another location before a new external replenishment order is created. Microsoft documents transfers as a source of supply for locations and describes planning systems that can generate transfer requirements from an assigned source warehouse.[^1][^2]

## Purpose

The purpose is to use stock that is already available inside the organisation before purchasing additional units from a supplier.

For example, if Branch A is approaching its reorder point while Branch B has excess units of the same item, the feature can identify Branch B as a possible source and recommend an internal transfer. This can reduce unnecessary external purchasing while keeping the destination supplied.

## How It Works

1. The system identifies a location whose inventory position requires replenishment.
2. It searches other approved locations for available quantities of the same item.
3. For each possible source location, it checks available stock after considering that location's existing demand and committed quantities.
4. It checks whether the source-to-destination transfer route is allowed.
5. It estimates the transfer arrival date using the configured transport time for the route. Microsoft documents transport days between shipping and receiving warehouses for transfer planning.[^1]
6. It compares the possible transfer quantity with the destination's replenishment need.
7. If a suitable source is found, the system creates a transfer recommendation instead of immediately relying on an external purchase recommendation.
8. The recommendation records the source location, destination location, quantity, and expected receipt date.
9. The system tracks the transfer as incoming supply to the destination while the units are in transit.
10. If no suitable internal source exists, the destination remains available for the normal external replenishment process.

## Information Required

- Item or SKU
- Destination location
- Destination inventory position and replenishment need
- Available stock at other locations
- Demand or committed quantities at source locations
- Approved transfer routes
- Transfer transport time
- Transfer quantity or quantity that can safely be moved
- Existing transfer orders or other incoming supply

## Output / Action

- Recommended source location
- Recommended destination location
- Recommended transfer quantity
- Expected transfer receipt date
- Transfer-review event or transfer order proposal
- Reason why an internal transfer could not be recommended, when no suitable source exists

## Benefits

- Uses existing inventory before buying additional stock externally.
- Helps balance stock between locations.
- Can provide a supply option when another location has inventory available sooner than an external supplier.
- Makes the source, quantity, route, and expected receipt date visible before a transfer is approved.[^2]

## Limitations / Dependencies

- The feature requires multiple inventory locations and defined transfer routes.
- Source inventory must be accurate; transferring stock that is already committed elsewhere can create a new shortage.
- Transport time and route data must be maintained accurately.
- The recommendation does not remove the need to consider supplier replenishment when no suitable internal source is available.
- A transfer can move a shortage from one location to another if the source's future demand is not considered.

## Sources

- Microsoft Learn, [Set up warehouses for transfer orders](https://learn.microsoft.com/en-us/dynamics365/supply-chain/warehousing/transfer-orders-warehouse). Accessed 30 September 2026.
- Microsoft Learn, [Design details: Transfers in planning](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-transfers-in-planning). Accessed 30 September 2026.
- Microsoft Learn, [Walkthrough: Planning supplies manually](https://learn.microsoft.com/en-us/dynamics365/business-central/walkthrough-planning-supplies-manually). Accessed 30 September 2026.

[^1]: Microsoft documents warehouse refilling through planned transfer orders and the use of transport days between shipping and receiving warehouses.
[^2]: Microsoft documents transfer inventory as a source of supply and shows an available-for-transfer alternative when another location has the needed stock.
