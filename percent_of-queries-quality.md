
# SQL Problem: 1211. Queries Quality and Percentage

## Problem Description
Write a solution to find each query_name, the quality and poor_query_percentage.

Both quality and poor_query_percentage should be rounded to 2 decimal places.

Return the result table in any order.

We define query quality as:

`The average of the ratio between query rating and its position.`

We also define poor query percentage as:

`The percentage of all queries with rating less than 3.`


## Table Schema

### Queries



| Column Name | Type    |
|------------|---------|
| query_name  | varchar |
| result      | varchar |
| position    | int     |
| rating      | int     |

- This table may have duplicate rows.
- This table contains information collected from some queries on a database.
- The position column has a value from `1` to `500`.
- The rating column has a value from `1 to 5`. Query with rating `less than 3` is a poor query.

## SQL Solution
```sql
SELECT query_name, 
    ROUND(AVG(rating*1.00/position),2) as quality,
    ROUND(SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END )*100.00 / count(*),2) as percent_poor_query
FROM Queries
GROUP BY query_name; 
```
