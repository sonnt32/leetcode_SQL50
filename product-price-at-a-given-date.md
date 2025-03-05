# 1164. Product Price at a Given Date

```sql

WITH t1 AS (
    select product_id, max(change_date) over (partition by product_id) as last_date
    FROM Products
    WHERE change_date <= '2019-08-16'
)

SELECT t1.product_id, p.new_price price
FROM Products p
JOIN t1 ON
    t1.product_id = p.product_id
AND t1.last_date = p.change_date

UNION

SELECT product_id,10 price
FROM Products
WHERE product_id NOT IN (select product_id from t1)
```
