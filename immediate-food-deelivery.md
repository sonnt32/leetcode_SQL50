## 1174. Immediate Food Delivery II

### SQL Solution
```sql
SELECT ROUND(100.0 *
SUM(CASE WHEN order_date = customer_pref_delivery_date THEN 1 ELSE 0 END) / COUNT (*) , 2)
as immediate_percentage
FROM (
    SELECT MIN (order_date) as order_date, MIN (customer_pref_delivery_date) as customer_pref_delivery_date
    FROM Delivery
    Group by customer_id
) AS A
```
