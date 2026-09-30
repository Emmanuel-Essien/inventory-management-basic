# Supplier Lead Time Monitoring

## Description

Supplier Lead Time Monitoring is a Smart Reordering feature that records and monitors how long suppliers actually take to deliver replenishment orders. It compares expected delivery time with actual delivery time and makes current lead-time information available to the reordering process.

## Purpose

The purpose is to keep supplier lead-time information accurate. Reorder decisions depend on how long replenishment takes, so outdated lead-time values can cause orders to be placed too late or too early.

## How It Works

1. Store the expected lead time for each item-supplier relationship.
2. When a replenishment order is created, record the order date and expected delivery date.
3. When the order is received, record the actual delivery date.
4. Calculate the actual lead time from the order and receipt dates.
5. Compare actual lead time with the stored expected lead time.
6. Maintain recent delivery history so repeated delays or improvements can be identified.
7. Flag a supplier or item when actual lead time consistently differs from the value being used for reordering.
8. Provide the updated information to reorder-point calculations or require a person to approve a change before the stored lead time is changed.

## Information Required

- Supplier
- Item and location or SKU
- Purchase or replenishment order date
- Expected delivery date
- Actual receipt date
- Current stored supplier lead time
- Historical delivery times
- Optional information such as partial deliveries, cancelled orders, and supplier-specific exceptions

## Output / Action

- Current expected lead time for each supplier-item relationship
- Actual delivery-time history
- Difference between expected and actual lead time
- An alert when delivery performance repeatedly exceeds the stored lead time
- A suggested lead-time update or a request for manual review
- Information that can be used by Reorder Point Monitoring when calculating demand during lead time

## Benefits

- Reduces reliance on outdated supplier lead-time values.
- Helps identify suppliers whose deliveries regularly arrive later than expected.
- Gives the reorder process better information about when replenishment is likely to arrive.
- Provides a record that can help explain why reorder settings were changed.

## Limitations / Dependencies

- Actual lead time cannot be measured accurately if purchase orders or receipt dates are missing or incorrect.
- Partial deliveries need a defined rule because the first receipt and complete receipt may have different dates.
- A single unusually late delivery may not represent the supplier's normal performance.
- Changing the stored lead time automatically can affect reorder decisions, so a manual approval step may be appropriate.
- The feature depends on accurate supplier, purchase-order, and goods-receipt records.

## Sources

- Microsoft Learn, [Design details: Handling reordering policies](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-handling-reordering-policies). Accessed 30 September 2026.
- SAP Learning, [Using Forecast in Reorder Point Planning](https://learning.sap.com/courses/consumption-based-planning-and-forecasting-in-sap-cloud-erp/using-forecast-in-reorder-point-planning). Accessed 30 September 2026.
