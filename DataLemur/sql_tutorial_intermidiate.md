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
- **NULL:** COALESCE(), IFNULL()
- **NULL** = the smallest value in SQL sorting order
- **COALESCE():** Versatile for multiple arguments, it returns the first non-null value among them. COALESCE(arg1, arg2, arg3, ...)
- **IFNULL():** Handles two arguments, returning the second if the first is null; else, it returns the first. IFNULL(expression, value_if_null)
- **CASE + SELECT:** create new columns, categorize data, or perform calculations based on specified conditions.
- **CASE + WHERE:** filter rows based on specified conditions within the dataset.
- CASE -> WHEN -> THEN -> ELSE ->  END
- COUNT() + CASE: COUNT( CASE WHEN ... THEN 1 ELSE NULL)
- 

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

12) [Unfinished Parts](https://datalemur.com/questions/tesla-unfinished-parts)
   ```sql
      SELECT part, 
         assembly_step
      FROM parts_assembly
      WHERE finish_date IS NULL
   ```

13) [SQL Tutorial Lesson: Superheroes' Likes](https://datalemur.com/questions/sql-case-marvel-avengers)
   ```sql
      SELECT actor, 
       character,
       platform, 
       avg_likes,
       CASE
           WHEN avg_likes >= 15000 THEN 'Super Likes'
           WHEN avg_likes BETWEEN 5000 AND 14999 THEN 'Good Likes'
           ELSE 'Low Likes'
      END AS likes_category
      FROM marvel_avengers 
      ORDER BY avg_likes DESC
   ```

14) [Laptop vs. Mobile Viewership](https://datalemur.com/questions/laptop-mobile-viewership)
   ```sql
      SELECT 
          SUM(CASE WHEN device_type = 'laptop' THEN 1 ELSE 0 END) AS laptop_reviews,
          SUM(CASE WHEN device_type IN ('tablet','phone') THEN 1 ELSE 0 END) AS mobile_views
      FROM viewership
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

