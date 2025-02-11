
# SQL Problem: 1251. Average Selling Price

## Problem Description
Each product has a price that varies over different time periods. The `Prices` table records these changes without any overlapping periods for the same product. The `UnitsSold` table tracks the number of units sold for each product on a given date. The goal is to compute the average selling price for each product, rounding the result to two decimal places. If a product has no sales, its average selling price should be 0.

## Table Schema

Prices Table

| Column Name | Type |
|------------|------|
| product_id | int  |
| start_date | date |
| end_date   | date |
| price      | int  |

- `(product_id, start_date, end_date)` is the primary key.
- Each row represents the price of a product over a specific date range.
- There are no overlapping periods for the same product.

 UnitsSold Table

| Column Name | Type |
|------------|------|
| product_id | int  |
| purchase_date | date |
| units | int |

- Each row represents a sale transaction, including the product ID, purchase date, and units sold.
- The table may contain duplicate rows.

## SQL Solution

```sql
WITH Us AS (
    SELECT u.product_id, 
           u.purchase_date, 
           u.units, 
           p.price
    FROM UnitsSold u
    LEFT JOIN Prices p
    ON p.product_id = u.product_id 
    AND u.purchase_date BETWEEN p.start_date AND p.end_date
)

SELECT product_id, 
       ROUND(COALESCE(SUM(CAST(units AS DECIMAL(10,2)) * price) / NULLIF(SUM(CAST(units AS DECIMAL(10,2))), 0), 0), 2) 
       AS average_price
FROM Us
GROUP BY product_id;
```

## Explanation of the Query
- The `WITH Us` common table expression (CTE) joins the `UnitsSold` table with the `Prices` table to associate each sale with the correct product price based on the purchase date.
- The main query calculates the total revenue for each product by multiplying `units` by `price` and summing the values.
- The average selling price is computed as `total revenue / total units sold`, using `COALESCE` and `NULLIF` to handle cases where a product has no sales.
- The result is rounded to two decimal places to meet the problem's requirements.

This solution ensures that all products appear in the final output, even those without any sales.

