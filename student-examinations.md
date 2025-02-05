# SQL Problem: 1280. Students and Examinations

## Problem Description:
In a school, there is a list of students and a list of subjects. Each student may attend multiple examinations for each subject. The goal is to write an SQL query to find the number of times each student attended an exam for each subject.

The result table should include `student_id`, `student_name`, `subject_name`, and the number of times the student attended the exam (`attended_exams`). The output should be sorted by `student_id` and `subject_name`.

## Table Schema:

### Students Table:
| Column Name   | Type    |
|--------------|---------|
| student_id   | int     |
| student_name | varchar |

- `student_id` is the primary key of this table.
- Each row represents a student in the school.

### Subjects Table:
| Column Name  | Type    |
|-------------|---------|
| subject_name | varchar |

- `subject_name` is the primary key of this table.
- Each row contains the name of a subject in the school.

### Examinations Table:
| Column Name  | Type    |
|-------------|---------|
| student_id  | int     |
| subject_name | varchar |

- There is no primary key; this table may contain duplicate records.
- Each row represents an instance of a student attending an exam for a subject.

## SQL Solution:
```sql
WITH FULL_TABLE AS (
    SELECT s.student_id, s.student_name, sub.subject_name
    FROM Students s
    CROSS JOIN Subjects sub
)

SELECT 
    f.student_id, 
    f.student_name, 
    f.subject_name, 
    COUNT(e.student_id) AS attended_exams
FROM FULL_TABLE f
LEFT JOIN Examinations e
ON f.student_id = e.student_id AND f.subject_name = e.subject_name
GROUP BY f.student_id, f.student_name, f.subject_name
ORDER BY f.student_id, f.subject_name;
```

## Explanation of the Query:
This query works as follows:
- Create a `FULL_TABLE` containing all possible student-subject pairs using a `CROSS JOIN` between `Students` and `Subjects`. This ensures that every student appears with every subject, even if they did not attend any exams.
- Use a `LEFT JOIN` to merge `FULL_TABLE` with the `Examinations` table based on `student_id` and `subject_name`. If a student has attended an exam for a particular subject, the `Examinations` table will have corresponding records; otherwise, it will contain `NULL`.
- Use `COUNT(e.student_id)` to count the number of times a student attended an exam for each subject. Since we use `LEFT JOIN`, students who did not attend any exams will have a count of `0`.
- Finally, group the results by `student_id`, `student_name`, `subject_name`, and sort them by `student_id` and `subject_name` to ensure proper ordering.

The final output ensures that all students appear in the result along with all subjects, even if they did not attend any exams.

