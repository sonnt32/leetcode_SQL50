# 1204. Last Person to Fit in the Bus

``` sql

SELECT TOP 1(person_name) 
FROM (SELECT *, SUM(weight) OVER (ORDER BY turn) as total_weight
FROM Queue) A
ORDER BY (ABS(total_weight - 1000))
```
