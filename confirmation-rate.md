
# SQL Problem: 1934. Confirmation Rate

## Table Schema

### Signups Table
```
| Column Name | Type     |
|------------|----------|
| user_id    | int      |
| time_stamp | datetime |
```

### Confirmations Table
```
| Column Name | Type     |
|------------|----------|
| user_id    | int      |
| time_stamp | datetime |
| action     | ENUM     |
```

## SQL Solution
```sql
WITH cf AS (
    SELECT user_id,
        COUNT(*) AS so_request,
        SUM(CASE WHEN action = 'confirmed' THEN 1 ELSE 0 END) AS so_thanh_cong
    FROM Confirmations
    GROUP BY user_id
)
SELECT s.user_id,
ROUND(COALESCE (c.so_thanh_cong,0)*1.0 /COALESCE(NULLIF(c.so_request,0),1),2) as confirmation_rate
FROM Signups s
LEFT JOIN cf as c ON s.user_id = c.user_id
ORDER BY s.user_id;
```

## Explanation of the Query
- Create a common table expression (`cf`) to compute the number of confirmation requests (`so_request`) and successful confirmations (`so_thanh_cong`) per user.
- Use `LEFT JOIN` to ensure all users from the `Signups` table appear in the result, including those who never requested a confirmation.
- Calculate the confirmation rate as `so_thanh_cong / so_request`, handling cases where `so_request` is `0` using `COALESCE` and `NULLIF` to prevent division by zero.
- Round the result to two decimal places for consistency.
- The final result is sorted by `user_id` to match the expected output format.
