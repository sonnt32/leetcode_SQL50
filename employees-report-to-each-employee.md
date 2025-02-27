# 1731. The Number of Employees Which Report to Each Employee

```sql
SELECT e1.employee_id, e1.name, count(e2.reports_to) as reports_count, 
ROUND(
    CAST(SUM(e2.age) AS FLOAT) 
    / 
    CAST(COUNT(e2.age) AS FLOAT), 0) AS average_age
FROM Employees e1
INNER JOIN Employees e2
ON e1.employee_id = e2.reports_to
GROUP BY e1.employee_id, e1.name
ORDER BY e1.employee_id
```
