# 1045. Customers Who Bought All Products
``` sql

SELECT customer_id 
from Customer
GROUP BY customer_id
HAVING count(distinct product_key) = (
    SELECT count(product_key) from Product
)

```
