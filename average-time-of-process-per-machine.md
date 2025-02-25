# SQL Problem: 1661. Average Time of Process per Machine
## Table Schema:
| Column Name    | Type    |
|----------------|---------|
| machine_id     | int     |
| process_id     | int     |
| activity_type  | enum    |
| timestamp      | float   |

## SQL solution:
```sql
WITH MACHINE_OVER AS (
    SELECT 
        machine_id, 
        process_id, 
        MAX(CASE WHEN activity_type = 'end' THEN timestamp ELSE NULL END) AS time_end,
        MIN(CASE WHEN activity_type = 'start' THEN timestamp ELSE NULL END) AS time_start
    FROM Activity
    GROUP BY machine_id, process_id
),
TIME_XU_LY AS (SELECT 
    machine_id, 
    process_id, 
    time_end - time_start AS time_xu_ly
FROM MACHINE_OVER)

SELECT machine_id, avg(time_xu_ly) as processing_time
FROM TIME_XU_LY
GROUP BY machine_id
```

## Explanation Query:
This query shows the average amount of time the machine needs to run several processes.
