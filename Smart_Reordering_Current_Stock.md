# Current Stock

## Checks the current stock of the product and returns it based on sales history

## Purpose
- Let's the business know how much of a certain product/item is available

## How It Works
- Checks the `product_id`
- Checks database for par-level
- Gets `order_history` for `product_id`
- Checks sales history for `product_id`
- removes values from `sales_history` since last order
- return result

## Information Required
- `product_id`: the unique id for a product
- `par_level`: the amount of a product the supplier aims to have in stock
- `order_history`: History of orders
- `sales_history`: Sales made

## Output / Action
- Returns the amount of goods in inventory

## Benefits
- Gives the value of the items left in inventory
- Removes need for manually counting

## Limitations / Dependencies
- Could be verbose in Java
- Would have to only take in certain datatypes as parameters

## Sources

- Oracle ordering system
- Amazon reordering system documentation
