## SQL Problem: 1193. Monthly Transactions I

## Problem Description
Write an SQL query to find, for each month and country:
- The number of transactions and their total amount.
- The number of approved transactions and their total amount.

Return the result table in any order.

## Table Schema

### Table: Transactions


| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| country       | varchar |
| state         | enum    |
| amount        | int     |
| trans_date    | date    |


- `id` is the primary key of this table.
- The table has information about incoming transactions.
- The `state` column is an `ENUM` of type `["approved", "declined"]`.

## Example

### Input
`Transactions table`

| id   | country | state    | amount | trans_date |
|------|---------|----------|--------|------------|
| 121  | US      | approved | 1000   | 2018-12-18 |
| 122  | US      | declined | 2000   | 2018-12-19 |
| 123  | US      | approved | 2000   | 2019-01-01 |
| 124  | DE      | approved | 2000   | 2019-01-07 |

## SQL Solution

```sql
SELECT 
    DATE_FORMAT(trans_date, '%Y-%m') AS month, 
    country, 
    COUNT(*) AS trans_count, 
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM Transactions
GROUP BY month, country;
```

## Explanation of the Query
- `DATE_FORMAT(trans_date, '%Y-%m')`: Extracts the year and month from `trans_date`.
- `COUNT(*)`: Counts the total number of transactions.
- `SUM(amount)`: Calculates the total transaction amount.
- `SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END)`: Counts the number of approved transactions.
- `SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END)`: Sums the total amount of approved transactions.
- `GROUP BY month, country`: Groups the results by month and country.
