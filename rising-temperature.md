# SQL Problem: 197. Rising Temperature

## Problem Description
- Write a solution to find all dates `id`  with higher temperatures compared to its previous dates (yesterday).
- Return the result table in any order.
- The result format is in the following example.

## Table:

| id | recordDate | temperature |
|----|------------|-------------|
| `1`  | 2015-01-01 | 10          |
| `2`  | 2015-01-02 | 25          |
| `3`  | 2015-01-03 | 20          |
| `4`  | 2015-01-04 | 30          |

## SQL Solution:
``` sql
WITH data AS (
    SELECT id, recordDate, temperature, 
           LAG(temperature) OVER (ORDER BY recordDate) AS hom_truoc
    FROM Weather
)
SELECT id
FROM data
WHERE temperature > hom_truoc;

```
## Explanation:

- This query shows the ID of the date where today's temperature is higher than yesterday's.
- I used the LAG() function to select the date and its temperature from yesterday.
