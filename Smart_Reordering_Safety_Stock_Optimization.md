# Smart Reordering — Safety Stock Optimization

## Objective
Calculate a recommended safety stock level for each inventory item using demand variability, supplier lead-time variability, and a target service level.

## Business Value
Safety stock provides protection against uncertainty in demand and replenishment time. This feature gives the inventory team a consistent method for estimating the buffer required to reduce stockout risk.

## Inputs
- SKU or item identifier
- Average demand per period
- Standard deviation of demand
- Average supplier lead time
- Standard deviation of supplier lead time
- Target service level

## Calculation
For variable demand and variable lead time, estimate lead-time demand variability as:

\[
\sigma_{LT}=\sqrt{(L\times\sigma_d^2)+(d^2\times\sigma_L^2)}
\]

Then calculate:

\[
Safety\ Stock=z\times\sigma_{LT}
\]

where z is the standard normal value associated with the selected target service level.

## Expected Output
For each SKU:
- Recommended safety stock quantity
- Target service level
- Demand variability
- Lead-time variability
- Current versus recommended safety stock
- Review flag when the recommendation changes materially

## Process
1. Collect historical demand and supplier lead-time records.
2. Calculate average demand and demand variability.
3. Calculate average lead time and lead-time variability.
4. Select the target service level.
5. Calculate lead-time demand variability.
6. Calculate the recommended safety stock.
7. Compare it with the current setting and flag the item for review.

## Limitations
The method relies on historical averages and standard deviations. Intermittent, highly seasonal, or strongly skewed demand may require a different statistical approach. The recommendation should support inventory review rather than automatically changing purchasing policy.

## Source
Oracle Supply Chain documentation:
https://docs.oracle.com/en/cloud/saas/supply-chain-and-manufacturing/25d/faupc/safety-stock.html
