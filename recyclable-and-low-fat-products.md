# SQL Problem: 1757. Find Low Fat and Recyclable Products

## Problem Description

Write a query to find the **IDs** of products that satisfy the following conditions:
- The product is **low fat**.
- The product is **recyclable**.

Return the result table in **any order**.

---

## Table Schema

| Column Name   | Type    | Description                                                                                     |
|---------------|---------|-------------------------------------------------------------------------------------------------|
| `product_id`  | `int`   | **Primary key** (unique identifier for each product).                                           |
| `low_fats`    | `enum`  | - `'Y'`: Indicates the product is low fat. <br> - `'N'`: Indicates the product is not low fat.   |
| `recyclable`  | `enum`  | - `'Y'`: Indicates the product is recyclable. <br> - `'N'`: Indicates the product is not recyclable.|

---

## SQL Solution

```sql
SELECT product_id
FROM products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```

---
