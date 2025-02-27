# 596. Classes More Than 5 Students

```sql
SELECT b.class as class
FROM (
    SELECT class
    FROM Courses
    /*where nếu lọc trước khi count student*/
    GROUP BY class
    HAVING count(student) > 5
) AS b
```
