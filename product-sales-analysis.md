# SQL Problem: 1068. Product Sales Analysis I

# Problem description:
Write a solution to report:
- the product_name, year, and price for each sale_id in the Sales table.
- Return the resulting table in any order.

## Table schema:
1. `**Sale**` table:


| Column Name | Type  | Description |
|-------------|-------| --|
| `sale_id `   | `int  ` | p.key |
| `product_id ` |` int`   | |
| `year    `    |` int   `| p.key|
|` quantity   ` |` int  ` ||
| `price     `  |` int   `||

Demo input:

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------| 
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

2. `**Product**` table


| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

## SQL Solution:

SELECT Product.product_name, Sales.year,Sales.price
FROM Sales
WHERE 
