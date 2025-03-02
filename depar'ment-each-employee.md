# 1789. Primary Department for Each Employee

```sql
SELECT employee_id, department_id
FrOM Employee
WHEre primary_flag = 'Y' OR employee_id IN
( SELECT employee_id 
FrOM Employee
Group by employee_id
HAVING count(*) =1)
```
