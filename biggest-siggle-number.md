# Biggest Single Number

```sql

SELECT MAX(num) as num
FROM (
    SELECT num
    FROM MyNumbers
    GROUP BY num
    HAVING count(num) = 1
    ) A
```
