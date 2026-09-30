# Budget-Constrained Reordering

## Description

Budget-Constrained Reordering is a Smart Reordering feature that recommends replenishment orders while considering the amount of money available for purchasing inventory. Instead of treating every item as equally reorderable, the feature prioritizes products when the available purchasing budget cannot cover all desired replenishment quantities.

## Purpose

The feature addresses situations where a business has limited cash available for inventory purchases. Without a budget constraint, a reorder system may recommend quantities that are operationally appropriate but financially impossible to purchase. The feature helps the system make replenishment recommendations that fit within a defined purchasing budget while considering inventory needs and stockout risk.

## How It Works

The system first calculates the normal replenishment requirement for each product using information such as current stock, expected demand, lead time, and the target inventory level. It then compares the total estimated purchase cost with the available budget.

If the required purchase cost is within the budget, the system can approve the normal recommendations. If the cost exceeds the budget, the system ranks or prioritizes products using rules such as urgency, expected demand, stockout risk, and unit purchase cost. It then reduces or postpones lower-priority purchases until the recommended order fits the available budget.

The feature can also allow the user to set a minimum budget reserve so that the system does not recommend spending the entire available amount.

## Information Required

- Current inventory levels for each product
- Forecast or expected demand
- Reorder point or target stock level
- Supplier lead time
- Unit purchase cost
- Available purchasing budget
- Minimum budget reserve, if applicable
- Stockout risk or product priority
- Existing outstanding purchase orders

## Output / Action

The feature produces a budget-aware replenishment plan. It can recommend which products to reorder, the quantity to order, and which lower-priority purchases should be reduced or postponed when the budget is insufficient.

It can also generate an alert when the estimated replenishment requirement exceeds the available budget.

## Benefits

- Prevents replenishment recommendations from exceeding the available purchasing budget.
- Helps prioritize critical products when funds are limited.
- Reduces the risk of spending available cash on lower-priority inventory.
- Gives inventory managers a clearer basis for deciding which orders to place first.

## Limitations / Dependencies

The quality of the recommendation depends on accurate product costs, inventory records, demand estimates, and budget information. A budget-based recommendation may still leave some products below their preferred stock level when funds are insufficient. Business rules are also needed to determine which products should receive priority.

## Sources

- Ghalebsaz-Jeddi, B., Shultes, B. C., & Haji, R. (2004). A multi-product continuous review inventory system with stochastic demand, backorders, and a budget constraint. European Journal of Operational Research. https://doi.org/10.1016/S0377-2217(03)00363-1
- Springer Nature (2023). Sponsored search advertising and inventory replenishment: a decision support framework for an online retailer. https://link.springer.com/article/10.1007/s10479-023-05643-5
