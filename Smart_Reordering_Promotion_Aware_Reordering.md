# Promotion-Aware Reordering

## Description

Promotion-Aware Reordering is a Smart Reordering feature that adjusts replenishment recommendations when a product is affected by a planned promotion, discount, campaign, or other sales event. It recognizes that promotional activity can temporarily change normal demand and therefore can require a different inventory plan.

## Purpose

The feature addresses the risk of understocking products during promotions and overstocking them after the promotion ends. A normal reorder calculation based only on historical non-promotional demand may fail to account for a temporary increase in sales caused by a promotion.

## How It Works

The system identifies upcoming promotions and links them to the affected products. It reviews historical sales during similar promotional periods and compares them with normal demand.

The system then estimates the expected promotional demand and uses that estimate when calculating replenishment quantities. It considers the promotion dates, expected demand increase, current inventory, supplier lead time, and the expected inventory remaining after the promotion.

Before the promotion, the system can recommend additional replenishment when the projected stock is insufficient. After the promotion, it can reduce future replenishment recommendations if demand is expected to return toward its normal level.

## Information Required

- Historical sales data
- Normal baseline demand
- Promotion or campaign schedule
- Promotion start and end dates
- Discount or promotion type
- Products affected by the promotion
- Current inventory
- Supplier lead time
- Existing purchase orders
- Previous promotional sales data, when available

## Output / Action

The feature produces an adjusted demand estimate and promotion-aware reorder recommendation. It can recommend additional quantities before a promotion, alert users when projected inventory may be insufficient, and reduce replenishment after the promotion when demand is expected to normalize.

## Benefits

- Reduces the risk of stockouts during promotional periods.
- Helps the business prepare inventory for expected temporary demand increases.
- Reduces reliance on ordinary demand patterns when promotions are planned.
- Helps prevent unnecessary replenishment after promotional demand returns toward normal levels.

## Limitations / Dependencies

Promotional demand is difficult to predict because the response can vary by product, discount, timing, customer behavior, and competing products. Historical promotional data may not exist for new products or unusual campaigns. The feature also depends on receiving accurate promotion schedules and product information early enough to influence replenishment decisions.

## Sources

- Chaowai, K., & Chutima, P. (2024). Demand Forecasting and Ordering Policy of Fast-Moving Consumer Goods with Promotional Sales in a Small Trading Firm. Engineering Journal, 28(4). https://doi.org/10.4186/ej.2024.28.4.21
- Syntetos et al. (2020). Demand forecasting in supply chain: the impact of demand volatility in the presence of promotion. Computers & Industrial Engineering, 142, 106380. https://doi.org/10.1016/j.cie.2020.106380
- Halgamuwe Hewage, H., Perera, H. N., & Bandara, K. (2026). Enhancing demand forecasting in retail: A comprehensive analysis of sales promotion effects on the entire demand life cycle. Journal of Forecasting, 45(1), 293–315. https://doi.org/10.1002/for.70039
