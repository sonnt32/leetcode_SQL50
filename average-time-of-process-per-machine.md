# SQL Problem: 1661. Average Time of Process per Machine
## Problem Description:
- There is a factory website that has several machines each running the same number of processes. Write a solution to find the average time each machine takes to complete a process.
- The time to complete a process is the 'end' timestamp minus the 'start' timestamp. The average time is calculated by the total time to complete every process on the machine divided by the number of processes that were run.
The resulting table should have the machine_id along with the average time as processing_time, which should be rounded to 3 decimal places.

## Table Schema:
| Column Name    | Type    |
|----------------|---------|
| machine_id     | int     |
| process_id     | int     |
| activity_type  | enum    |
| timestamp      | float   |

*`Description Table:`*

The table shows the user activities for a factory website.

`(machine_id, process_id, activity_type)` is the primary key (combination of columns with unique values) of this table.

`machine_id` is the ID of a machine.

`process_id` is the ID of a process running on the machine with ID machine_id.

`activity_type` is an ENUM (category) of type ('start', 'end').

`timestamp` is a float representing the current time in seconds.

`'start'` means the machine starts the process at the given timestamp and `'end'` means the machine ends the process at the given timestamp.

The 'start' timestamp will always be before the 'end' timestamp for every (machine_id, process_id) pair.

It is guaranteed that each (machine_id, process_id) pair has a 'start' and 'end' timestamp.

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
