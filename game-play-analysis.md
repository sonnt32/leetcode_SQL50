
## 550. Game Play Analysis IV

## SQL SOLUTION
```sql

SELECT 
    ROUND(1.00* CAST(
        SUM(CASE WHEN DATEADD(day, 1, next_event_date) = event_date THEN 1 ELSE 0 END
) AS FLOAT)
        / (SELECT COUNT(DISTINCT player_id) FROM Activity),
    2) AS fraction
FROM (SELECT 
        player_id,
        event_date,
        LAG(event_date) OVER (PARTITION BY player_id ORDER BY event_date) AS next_event_date
    FROM Activity) AS A;
```
