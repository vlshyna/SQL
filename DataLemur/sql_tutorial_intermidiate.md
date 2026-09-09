Useful Links:
- [Data Lemur](https://datalemur.com/sql-tutorial)
- Book: [Ace The Data Science Interview](https://www.acethedatascienceinterview.com/)
- [SQL Interview Questions] (https://datalemur.com/sql-interview-questions)

</br>

Notes:
- **COUNT(column):** counts only the rows where the specified column is NOT NULL
- **COUNT(*):** counts every single row in the table or result set, regardless of whether its columns contain NULL values or duplicates.
- DISTINCT With Two Columns: all of the unique pairs of those two columns.

</br>

Tasks:
1) [Easy SQL GROUP BY Practice Exercise](https://datalemur.com/questions/sql-group-by-practice-exercise-easy)
    SELECT ticker, min(open) AS min
    FROM stock_prices
    GROUP BY ticker
    ORDER BY min desc

2) [SQL GROUP BY Practice Exercise: Candidate Skills](https://datalemur.com/questions/sql-group-by-practice-exercise-candidate-skills)
    SELECT skill, COUNT(candidate_id) AS count
    FROM candidates
    GROUP BY skill
    ORDER BY count DESC

3) [SQL HAVING MIN Practice Exercise](https://datalemur.com/questions/sql-having-min-practice-exercise)
   SELECT ticker, MIN(open) AS min
   FROM stock_prices
   GROUP BY ticker
   HAVING MIN(open) > 100

4) [SQL HAVING Practice Exercise](https://datalemur.com/questions/sql-having-practice-exercise)
    SELECT candidate_id
    FROM candidates
    GROUP BY candidate_id
    HAVING COUNT(skill) > 2

5) [Data Science Skills](https://datalemur.com/questions/matching-skills)
    SELECT candidate_id
    FROM candidates
    WHERE skill in ('Python','Tableau','PostgreSQL')
    GROUP BY candidate_id
    HAVING COUNT(*) = 3 
    ORDER BY candidate_id ASC

6) [SQL COUNT DISTINCT Practice Exercise](https://datalemur.com/questions/sql-count-distinct-practice-exercise)
    SELECT category, COUNT(DISTINCT product)
    FROM product_spend
    GROUP BY category

7) 
