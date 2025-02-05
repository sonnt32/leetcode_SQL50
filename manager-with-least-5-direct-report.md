# SQL Problem: 570. Managers with at Least 5 Direct Reports

## Problem Description:
- Given a table of employees with their respective managers, write a SQL query to find managers who have at least five direct reports.
- Each employee has a `managerId`, which indicates who their direct manager is.
- If `managerId` is `NULL`, it means that the employee does not have a manager.
- The result should return the `name` of the managers who meet the condition.

## Table Schema:

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |

**Description Table:**
- `id` is the primary key (unique identifier) of the table.
- Each row represents an employee, their department, and the ID of their direct manager.
- No employee can be their own manager.

## SQL Solution:
```sql
WITH manager_info AS (
    SELECT managerID, count(id) as so_nhan_vien
    FROM Employee
    WHERE managerID IS NOT NULL
    GROUP BY managerID
)
SELECT name 
FROM Employee
JOIN manager_info ON Employee.id = manager_info.managerID
WHERE so_nhan_vien >= 5
```

## Explanation Query:
- I first create a Common Table Expression (CTE) called manager_info that counts the number of employees (id) reporting to each manager (managerID).
- The WHERE managerID IS NOT NULL condition ensures that we only consider valid managers.
- I then group the results by managerID and count the number of direct reports as so_nhan_vien.
- In the main query, we join the Employee table with manager_info using Employee.id = manager_info.managerID.
- Finally, we filter out managers who have fewer than 5 direct reports using WHERE so_nhan_vien >= 5.

The query returns the name of managers who meet the criteria.
