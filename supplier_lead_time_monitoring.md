# Smart Reordering — Supplier Lead Time Monitoring

## Description

A feature that monitors supplier delivery times and uses them to improve when products should be reordered.

## Purpose

To prevent stockouts caused by late supplier deliveries.

## How It Works

1. Tracks previous supplier delivery times.
2. Compares expected and actual delivery dates.
3. Identifies suppliers with changing or delayed lead times.
4. Adjusts reorder timing based on the latest delivery patterns.
5. Alerts users when a delay may affect inventory levels.

## Information Required

- Supplier information
- Previous delivery dates
- Expected delivery dates
- Current inventory levels
- Product reorder points

## Output / Action

The system provides updated lead-time estimates and alerts users when a supplier delay could require an earlier reorder.

## Benefits

- Reduces stockout risk.
- Improves supplier monitoring.
- Supports better reorder timing.

## Limitations / Dependencies

- Requires accurate delivery records.
- Supplier performance can change unexpectedly.
- External disruptions may affect delivery times.

## Sources

- Oracle — Replenishment Planning
- SAP — Reorder Point Planning
