# SQL Problem: 584. Find Customer Referee

## Description problem

- Find the names of the customer that are not referred by the customer with id = 2.
- Return the result table in any order.

## Table schemas:

| Column Name   | Type    | Description                                                                                     |
|---------------|---------|-------------------------------------------------------------------------------------------------|
| `id`  | `int`   | **Primary key** (unique identifier for each product).                                           |
| `name`  | `varchae`   | customer name                                           |
| `referee_id`  | `int`   | id refereee                                       |

In SQL, id is the primary key column for this table.
Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.

---
## SQL solution (using SQL Server)
``` sql
SELECT name 
FROM Customer
WHERE referee_id is null or referee_id != 2
ORDER by name;
```

---
## Explanation
- **Result**: Return the customer name with a filter where referee_id is null (meaning the customers are not referred or not referred by another customer with id = 2).


