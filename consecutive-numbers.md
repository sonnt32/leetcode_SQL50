# 180. Consecutive Numbers

```sql

SELECT distinct num as ConsecutiveNums 
FROM (
SELECT id, num, 
LEAD(num) OVER (ORDER BY id) as hang_sau,
LAG(num) OVER (ORDER BY id) as hang_truoc
FROM Logs) A
WHERE num = hang_truoc and num = hang_sau
```
