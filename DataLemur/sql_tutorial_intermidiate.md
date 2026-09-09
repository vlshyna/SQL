Useful Links:
- [Data Lemur](https://datalemur.com/sql-tutorial)
- Book: [Ace The Data Science Interview](https://www.acethedatascienceinterview.com/)
- [SQL Interview Questions] (https://datalemur.com/sql-interview-questions)

</br>

Notes:
- **COUNT(column):** counts only the rows where the specified column is NOT NULL
- **COUNT(*):** counts every single row in the table or result set, regardless of whether its columns contain NULL values or duplicates.

</br>

Tasks:
1) [Easy SQL GROUP BY Practice Exercise](https://datalemur.com/questions/sql-group-by-practice-exercise-easy)
    SELECT ticker, min(open) AS min
    FROM stock_prices
    GROUP BY ticker
    ORDER BY min desc
