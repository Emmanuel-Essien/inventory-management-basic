# Supplier Capacity Monitoring

## Description

Supplier Capacity Monitoring evaluates whether a supplier is able to provide the quantity of an item required for replenishment within the expected time. It uses supplier information, available supply capacity, existing commitments, and the quantity required by the reordering process to identify potential supply constraints before an order is placed or confirmed.

## Purpose

The purpose of Supplier Capacity Monitoring is to identify situations where a supplier may not be able to fulfill a required replenishment quantity. This gives the reordering system information that can be used to avoid unrealistic replenishment plans, identify potential delays, and consider alternative suppliers or order arrangements when supply capacity is insufficient.

## How It Works

1. The system identifies the supplier associated with the item and the quantity required for replenishment.
2. It obtains relevant supplier capacity information, such as the supplier's available quantity, production or supply limits, and existing commitments.
3. The system compares the required replenishment quantity with the supplier's available capacity.
4. If the required quantity is within the available capacity, the replenishment request can proceed normally.
5. If the required quantity exceeds the available capacity, the system raises a capacity warning or identifies the quantity that may be supplied.
6. The system can pass the capacity information to the reordering process so that the order quantity or supplier decision can be reviewed.
7. Supplier capacity information can be updated as supplier commitments, available quantities, or replenishment requirements change.

## Information Required

- Item or SKU identifier
- Supplier identifier
- Required replenishment quantity
- Supplier available supply quantity or capacity
- Supplier production or supply limit, where applicable
- Existing supplier commitments