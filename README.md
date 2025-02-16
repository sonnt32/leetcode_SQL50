
# SQL Problem: 1633. Percentage of Users Attended a Contest

## Problem Description
We need to determine the percentage of users who registered for each contest. 

The percentage is calculated as the number of users registered for a contest divided by the total number of users. The result should be rounded to two decimal places.

## Table Schema

### Users Table

| Column Name | Type    |
|------------|---------|
| user_id    | int     |
| user_name  | varchar |

- `user_id` is the primary key.
- Each row contains the ID and name of a user.

### Register Table

| Column Name | Type |
|------------|------|
| contest_id | int  |
| user_id    | int  |

- `(contest_id, user_id)` is the primary key.
- Each row represents a user's registration in a specific contest.

## SQL Solution
```sql
WITH TotalUsers AS (
    SELECT COUNT(*) AS total_users FROM Users
)

SELECT
    r.contest_id,
    ROUND(COUNT(DISTINCT r.user_id) * 100.0 / tu.total_users, 2) AS percentage
FROM Register r
CROSS JOIN TotalUsers tu
GROUP BY r.contest_id, tu.total_users
ORDER BY percentage DESC, contest_id ASC;
```

## Explanation of the Query
1. Create a Common Table Expression (CTE) `TotalUsers` to calculate the total number of users.
2. Use `CROSS JOIN` to ensure each contest has access to the total number of users.
3. Count the distinct `user_id` values for each contest to determine how many users registered.
4. Compute the percentage by dividing the number of registered users by the total number of users, multiplying by 100, and rounding to two decimal places.
5. Order the results by `percentage` in descending order and by `contest_id` in ascending order in case of ties.


