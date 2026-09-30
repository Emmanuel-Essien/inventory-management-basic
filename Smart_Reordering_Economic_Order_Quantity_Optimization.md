# Smart Reordering Feature: Economic Order Quantity Optimization

## 1. Feature Description

Economic Order Quantity (EOQ) Optimization determines an appropriate quantity to order each time stock needs replenishment. It balances ordering costs with inventory holding costs to help determine an efficient replenishment quantity.

## 2. Purpose

The purpose of this feature is to recommend an economical order quantity that reduces unnecessary ordering and holding costs while maintaining an appropriate replenishment process.

## 3. How It Works

1. Collect the item's annual demand.
2. Determine the ordering cost for placing and receiving an order.
3. Determine the annual holding cost per unit.
4. Calculate the EOQ using:
   EOQ = √((2 × D × S) / H)
5. Round the result according to the item's ordering constraints.
6. Provide the recommended quantity to the replenishment process.
7. Allow the recommended quantity to be reviewed when business or supplier conditions change.

## 4. Inputs

- Item or SKU
- Annual demand
- Ordering cost per order
- Annual holding cost per unit
- Supplier or purchasing constraints
- Minimum order quantity where applicable

## 5. Outputs

- Recommended economic order quantity
- Calculation inputs used
- Rounded order quantity
- Review flag when supplier constraints affect the recommendation

## 6. Benefits

- Provides a structured basis for order quantities
- Balances ordering and holding costs
- Reduces arbitrary replenishment quantities
- Supports more consistent purchasing decisions

## 7. Limitations

- Requires reasonably accurate demand and cost information.
- The basic EOQ model assumes relatively stable demand and costs.
- Supplier minimum-order quantities may require adjustments.
- Discounts, shortages, seasonal demand, and other conditions may require additional rules.

## 8. Sources

- Oracle, Economic Order Quantity
- Microsoft Learn, Inventory and replenishment planning documentation
