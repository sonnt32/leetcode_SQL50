# SQL Problem: 1378. Replace Employee ID With The Unique Identifier

## Problem description:
Write a solution to show:
- the unique ID of each user
- If a user does not have a unique ID replace just show null.

Return the result table in any order.
The result format is in the following example.

## Table schema

### TABLE: EMPLOYEES

| Column Name   | Type    | Description                                                                                     |
|---------------|---------|-------------------------------------------------------------------------------------------------|
| `id`  | `int`   | **Primary key** (unique user).                                           |
| `name`    | `string`  | - Name of employee    |

Each row of this table contains the id and the corresponding unique id of an employee in the company.

Demo Input:

| id | name     |
|---|----------|
|` 1`  | `Alice`    |
| `7 ` | `Bob`      |
| `11` | `Meir`     |
| `90 `| `Winston`  |
| `3`  | `Jonathan` |



### TABLE: EmployeeUNI

| Column Name   | Type    | Description |
|-------------|----------|-------------|
| id            | int     | ID employee |
| unique_id     | int     | |

(id, unique_id) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id and the corresponding unique id of an employee in the company.

Demo output:

| Column Name   | Type    |
|---------------|---------|
| `3`  | `1`         |
| `11` | `2`         |
| `90` | `3`         |


## SQL Solution:

```sql
SELECT Employees.name, EmployeeUNI.unique_id
FROM Employees
LEFT JOIN EmployeeUNI ON Employees.id =  EmployeeUNI.id
```
## Explanation:
This query shows the employees' names and their unique IDs. If an employee does not have a unique ID, I display null
