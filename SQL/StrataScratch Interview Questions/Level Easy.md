```sql
--1) Find all posts which were reacted to with a heart. For such posts output all columns from facebook_posts table.

SELECT
  DISTINCT post.post_id,
           post.poster,
           post.post_text,
           post.post_keywords,
           post.post_date
FROM facebook_reactions AS react
INNER JOIN facebook_posts AS post
    ON react.post_id = post.post_id
WHERE reaction = 'heart'


--2) We have a table with employees and their salaries; however, some of the records are old and contain outdated salary information. Since there is no timestamp, assume salary is non-decreasing over time. You can consider the current salary for an employee is the largest salary value among their records. If multiple records share the same maximum salary, return any one of them. Output their id, first name, last name, department ID, and current salary. Order your list by employee ID in ascending order.

WITH
  row_num_table AS (
    SELECT
        id,
        first_name,
        last_name,
        department_id,
        salary,
        ROW_NUMBER() OVER (PARTITION BY id ORDER BY salary DESC) AS row_num
    FROM ms_employee_salary
)

SELECT
    id,
    first_name,
    last_name,
    department_id,
    salary
FROM row_num_table
WHERE row_num = 1
ORDER BY id

```
