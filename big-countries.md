# SQL Problem: 595. Big Countries

## Problem Description
- Write a solution to find the name, population, and area of the big countries.
- Return the result table in any order.
- The result format is in the following example.

A country is big if:
- it has an area of at least three million (i.e., 3000000 km2)
  OR
- it has a population of at least twenty-five million (i.e., 25000000).

## Table Schema:
| Column name | Type | Description |
|--------|----------------|------------------------|
|name| varchar | country name |
| continent   | varchar | continent of country |
| area        | int     | |
| population  | int     | |
| gdp         | bigint  | |

## SQL Solution (using SQL Server)
```
SELECT name, population, area
FROM World
WHERE area > 3000000 or population > 25000000
```

## Explanation
**Results**: That query select the country name, population and area in **World** table with a filter area > 3000000 km2 or population > 25000000 people
