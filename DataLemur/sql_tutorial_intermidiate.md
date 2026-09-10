Useful Links:
- [Data Lemur](https://datalemur.com/sql-tutorial)
- Book: [Ace The Data Science Interview](https://www.acethedatascienceinterview.com/)
- [SQL Interview Questions] (https://datalemur.com/sql-interview-questions)

</br>

Notes:
- **COUNT(column):** counts only the rows where the specified column is NOT NULL.
- **COUNT(*):** counts every single row in the table or result set, regardless of whether its columns contain NULL values or duplicates.
- **DISTINCT With Two Columns:** all of the unique pairs of those two columns.
- **ABS():** returns absolute value.
- **ROUND():** rounds a number to a specified number of decimal places.
- **CEIL():** round up (224.24 -> 225).
- **FLOOR()** round down (224.74 -> 224).
- **POWER():** ^, raises a number to a specified power.
- **MOD():** %, calculates the remainder of division between two numbers.
- int / int = int
- **Decimal/Float Output:** CAST(10 AS DECIMAL/FLOAT), multiplying by `1.0`, being explicit with types using `::`,  10::DECIMAL/4,
  10::FLOAT/4,
- **Calculate Percentages:** (part / total) * 100

</br>

Tasks:
1) [Easy SQL GROUP BY Practice Exercise](https://datalemur.com/questions/sql-group-by-practice-exercise-easy)
    ```sql
    SELECT ticker, min(open) AS min
    FROM stock_prices
    GROUP BY ticker
    ORDER BY min desc
    ```

2) [SQL GROUP BY Practice Exercise: Candidate Skills](https://datalemur.com/questions/sql-group-by-practice-exercise-candidate-skills)
    ```sql
    SELECT skill, COUNT(candidate_id) AS count
    FROM candidates
    GROUP BY skill
    ORDER BY count DESC
    ```

3) [SQL HAVING MIN Practice Exercise](https://datalemur.com/questions/sql-having-min-practice-exercise)
    ```sql
   SELECT ticker, MIN(open) AS min
   FROM stock_prices
   GROUP BY ticker
   HAVING MIN(open) > 100
    ```

4) [SQL HAVING Practice Exercise](https://datalemur.com/questions/sql-having-practice-exercise)
    ```sql
    SELECT candidate_id
    FROM candidates
    GROUP BY candidate_id
    HAVING COUNT(skill) > 2
    ```

5) [Data Science Skills](https://datalemur.com/questions/matching-skills)
   ```sql
    SELECT candidate_id
    FROM candidates
    WHERE skill in ('Python','Tableau','PostgreSQL')
    GROUP BY candidate_id
    HAVING COUNT(*) = 3 
    ORDER BY candidate_id ASC
   ```

6) [SQL COUNT DISTINCT Practice Exercise](https://datalemur.com/questions/sql-count-distinct-practice-exercise)
    ```sql
    SELECT category, COUNT(DISTINCT product)
    FROM product_spend
    GROUP BY category
    ```

7) [Pharmacy Analytics (Part 1)](https://datalemur.com/questions/top-profitable-drugs)
   ```sql
    SELECT drug, (total_sales - cogs) AS total_profit
    FROM pharmacy_sales
    ORDER BY total_profit DESC
    LIMIT 3
   ```

8) [Cards Issued Difference](https://datalemur.com/questions/cards-issued-difference)
   ```sql
    SELECT card_name, 
           MAX(issued_amount) - MIN(issued_amount) AS difference
    FROM monthly_cards_issued
    GROUP BY card_name
    ORDER BY difference DESC
   ```

9) [SQL Math Practice Exercise: Big-Mover Months](https://datalemur.com/questions/sql-math-practice-exercise-big-mover-months)
   ```sql
        SELECT ticker, COUNT(*) as count
        FROM stock_prices
        WHERE ((close - open)/open * 100) > 10 
              OR ((close - open)/open * 100) < -10 
        GROUP BY ticker
        ORDER BY count DESC
   ```


10) [SQL CEIL Practice Exercise](https://datalemur.com/questions/sql-ceil-practice-exercise)
   ```sql
        SELECT drug, 
            CEIL(SUM(total_sales)/SUM(units_sold)) AS unit_cost
        FROM pharmacy_sales
        WHERE manufacturer = 'Merck'
        GROUP BY drug
        ORDER BY unit_cost ASC 
   ```


11) [Ad Campaign ROAS](https://datalemur.com/questions/ad-campaign-roas)
   ```sql
      SELECT advertiser_id,
             ROUND( (SUM(revenue)*1.0)/SUM(spend), 2) AS roas
      FROM ad_campaigns
      GROUP BY advertiser_id
      ORDER BY advertiser_id
      
   ```

12) []()
   ```sql

   ```

13) []()
   ```sql

   ```

14) []()
   ```sql

   ```

15) []()
   ```sql

   ```

16) []()
   ```sql

   ```

17) []()
   ```sql

   ```

