Useful Links:
- [DataLemur Tutorial](https://datalemur.com/sql-tutorial/advanced-sql-tutorial-intro)
- [Ultimate SQL Interview Guide For Data Scientists & Data Analysts](https://datalemur.com/blog/sql-interview-guide#practice-take-home-sql-interview-challenges)
- [SQL Formatter](https://www.dpriver.com/pp/sqlformat.htm)

<br>

Notes (Clean SQL Queries):
- **Use uppercase** for the SQL keywords and functions
- Use **snake case**
- Use short and meaningful names for tables, columns, and expressions (+AS for Aliases)
   ```sql
      SELECT 
        companies.ticker,
        AVG(prices.close) AS avg_close,
        ROUND(AVG(prices.close), 2) AS rounded_avg_close
      FROM stock_prices AS prices
      INNER JOIN public_listed_companies AS companies
        ON prices.ticker = companies.ticker
      WHERE EXTRACT(YEAR FROM prices.date) = 2022
      GROUP BY companies.ticker;
   ```
- Be consistent. Use spaces or tabs throughout. !You can also use a code formatter tool to automatically apply a style to your code!
- **Don't use `SELECT *` in your queries.** Instead, explicitly list the columns you need. (If you're new to a table and want to see every column, add a `LIMIT` clause to reduce the number of rows being generated:)
- Use JOINs and Aliases for Clarity
- Specify JOIN Types. Be clear about your JOIN types (INNER JOIN, LEFT JOIN, RIGHT JOIN, etc.) to improve query clarity.
- Format Dates Consistently. Use a consistent date format to prevent ambiguity: `'YYYY-MM-DD'` format
- Comment Wisely. Use comments to explain your queries, but avoid writing long ones between queries. Briefly explain each step for clarity. Use `--` to write single-line comments.  Use `/* ... */` for longer comments and make sure they add valuable insights.

<br>

Generic syntax of ranking functions:
```sql
SELECT 
  RANK() / DENSE_RANK() / ROW_NUMBER() OVER ( -- Compulsory expression
    PARTITION BY partitioning_expression -- Optional expression
    ORDER BY order_expression) -- Compulsory expression
FROM table_name;
   ```

<br>

ROW_NUMBER vs. RANK vs. DENSE_RANK
- `ROW_NUMBER():` This function assigns a unique sequential number to each row within a window. It's like numbering the rows in order.
- `RANK():` The RANK() function handles tied values by assigning the same rank to them. However, it may skip subsequent ranks, leaving gaps in the sequence.
- `DENSE_RANK():` Similar to RANK(), DENSE_RANK() also handles tied values by assigning the same rank. However, it does not skip ranks, resulting in no gaps in the sequence.

<br>

Time-series window functions:
- LEAD(): future, LAG(): past
 ```sql
  LEAD(column_name, offset) OVER (  -- Compulsory expression
  PARTITION BY partition_column -- Optional expression
  ORDER BY order_column) -- Compulsory expression
  
   ```

<br>
UNION, INTERCEPT, EXCEPT:
- `UNION`: combine tables VERTICALLY, `JOIN`: HORIZONTALLY
- `UNION ALL` keeps everything, including duplicates.
- `UNION` removes duplicates, so you get only the unique items.

<br>

Self-Joins Example
 ```sql
      SELECT
        b1.genre,
        b1.book_title AS current_book,
        b2.book_title AS suggested_book
      FROM goodreads AS b1
      INNER JOIN goodreads AS b2
        ON b1.genre = b2.genre
      WHERE b1.book_id != b2.book_id
      ORDER BY b1.book_title;

--------------------------------------------------

      SELECT
           b1.genre,
           b1.book_title AS current_book,
           b2.book_title AS suggested_book_1,
           b3.book_title AS suggested_book_2
         FROM goodreads AS b1
         INNER JOIN goodreads AS b2 
           ON b1.genre = b2.genre
         INNER JOIN goodreads as b3 
           ON b1.genre = b3.genre
         WHERE b1.book_id != b2.book_id
           AND b1.book_id != b3.book_id
           AND b2.book_id != b3.book_id
         ORDER BY b1.book_title,
         LIMIT 50; 
   ```
- INTERSECT: vertical inner join: (SELECT FROM) INTERSECT (SELECT FROM)
<br>

1) [Supercloud Customer](https://datalemur.com/questions/supercloud-customer)
   ```sql
    WITH super_customer AS (
    SELECT customer_id,
           COUNT(DISTINCT product_category) AS product_count
    FROM customer_contracts сustomer
    LEFT JOIN products 
           ON сustomer.product_id = products.product_id
    GROUP BY customer_id
    )

   SELECT customer_id
   FROM super_customer
   WHERE product_count = (
         SELECT COUNT(DISTINCT product_category) FROM products
   );
   ```

2) [Swapped Food Delivery](https://datalemur.com/questions/sql-swapped-food-delivery)
   ```sql
      WITH changed_id AS(
      SELECT item, 
            CASE
              WHEN order_id <> MAX(order_id) OVER () AND order_id%2=1 THEN order_id+1
              WHEN order_id <> MAX(order_id) OVER () AND order_id%2=0 THEN order_id-1
              ELSE order_id
            END AS new_id
      FROM orders 
      ORDER BY new_id
   )
   
   SELECT new_id, item
   FROM changed_id;
   ```

3) [Card Launch Success](https://datalemur.com/questions/card-launch-success)
   ```sql
    WITH launch_date AS (
     SELECT 
       card_name,
       issued_amount,
       MAKE_DATE(issue_year, issue_month, 1) AS issue_date,
       MIN(MAKE_DATE(issue_year, issue_month, 1)) OVER (
         PARTITION BY card_name) AS launch_date
     FROM monthly_cards_issued
   )
   
   SELECT 
     card_name, 
     issued_amount
   FROM launch_date
   WHERE issue_date = launch_date
   ORDER BY issued_amount DESC;
   ```

4) [Top 5 Artists](https://datalemur.com/questions/top-fans-rank)
   ```sql
   WITH top_cte AS(
     SELECT 
       artists.artist_name,
       DENSE_RANK() OVER (
         ORDER BY COUNT(songs.song_id) DESC) AS artist_rank
     FROM artists 
     INNER JOIN songs
       ON artists.artist_id = songs.artist_id
     INNER JOIN global_song_rank AS song_rank
       ON songs.song_id = song_rank.song_id
     WHERE song_rank.rank <= 10
     GROUP BY artists.artist_name 
   )
   
   SELECT artist_name, artist_rank
   FROM top_cte
   WHERE artist_rank <= 5;
   ```

5) [Histogram of Users and Purchases](https://datalemur.com/questions/histogram-users-purchases)
   ```sql
      WITH transaction_date_rank AS(
         SELECT DENSE_RANK() OVER (
                   PARTITION BY user_id ORDER BY transaction_date DESC) AS date_rank,
                user_id,
                COUNT(*) AS purchase_count,
                transaction_date
         
         FROM user_transactions
         GROUP BY user_id, transaction_date
       )
         
       SELECT transaction_date,
                user_id,
                purchase_count
       FROM transaction_date_rank
       WHERE date_rank=1
       ORDER BY transaction_date ASC

   ```


6) [Odd and Even Measurements](https://datalemur.com/questions/odd-even-measurements)
   ```sql
     WITH
         measurement_rank AS(
            SELECT 
                measurement_time::DATE as measurement_day,
                measurement_value,
                TO_CHAR(measurement_time,'YYYY-MM-DD') AS char_data,
                RANK() OVER (
                      PARTITION BY TO_CHAR(measurement_time,'YYYY-MM-DD')
                      ORDER BY measurement_time) AS measure_rank
            FROM measurements
         ), 
   
         measurement_sum AS(
            SELECT char_data, 
                   SUM(
                      CASE 
                          WHEN measure_rank%2=1 THEN measurement_value
                          ELSE 0
                      END
                   ) AS odd_sum, 
                   SUM(
                      CASE 
                          WHEN measure_rank%2=0 THEN measurement_value
                          ELSE 0
                      END
                   ) AS even_sum
            FROM measurement_rank
            GROUP BY char_data
   )
   
   SELECT char_data::TIMESTAMP AS measurement_day,
          odd_sum,
          even_sum
   FROM measurement_sum
    
   ```

Official Solution:
   ```sql
      WITH ranked_measurements AS (
        SELECT 
          CAST(measurement_time AS DATE) AS measurement_day, 
          measurement_value, 
          ROW_NUMBER() OVER (
            PARTITION BY CAST(measurement_time AS DATE) 
            ORDER BY measurement_time) AS measurement_num 
        FROM measurements
      ) 
      
      SELECT 
        measurement_day, 
        SUM(measurement_value) FILTER (WHERE measurement_num % 2 != 0) AS odd_sum, 
        SUM(measurement_value) FILTER (WHERE measurement_num % 2 = 0) AS even_sum 
      FROM ranked_measurements
      GROUP BY measurement_day;
   ```


7) [SQL Tutorial Lesson: Stock Performance](https://datalemur.com/questions/sql-bloomberg-stock-performance)
   ```sql
      SELECT EXTRACT(MONTH FROM date) as month,
             close,
             LEAD(close) OVER (ORDER BY date) - close AS difference_1m,
             LEAD(close,3) OVER (ORDER BY date) - close AS difference_3m
      FROM stock_prices 
      WHERE ticker = 'GOOG' AND EXTRACT(YEAR FROM date) = 2023
      LIMIT 10;
   ```


8) [Y-on-Y Growth Rate](https://datalemur.com/questions/yoy-growth-rate)
   ```sql
      WITH 
         year_spend AS(
             SELECT product_id,
                    SUM(spend) AS cur_total_spend,
                    EXTRACT(YEAR FROM transaction_date) AS year
             FROM user_transactions
             GROUP BY product_id, year
         ),
         
         prev_month AS(
             SELECT 
               product_id,
               cur_total_spend,
               year,
               LAG(cur_total_spend) OVER (PARTITION BY product_id ORDER BY year) AS prev_year_spend
             FROM year_spend
         )
         
         SELECT year,
                product_id,
                cur_total_spend,
                prev_year_spend,
               ROUND( (cur_total_spend - prev_year_spend)/prev_year_spend * 100,2) AS yoy_rate
         FROM prev_month
       
   ```

9) [Well Paid Employees](https://datalemur.com/questions/sql-well-paid-employees)
   ```sql
      SELECT emp.employee_id AS emp_id,
             emp.name AS emp_name
      FROM employee AS mgr
      INNER JOIN employee AS emp 
        ON mgr.employee_id=emp.manager_id
      WHERE emp.salary > mgr.salary
   ```

1) []()
   ```sql

   ```

1) []()
   ```sql

   ```

1) []()
   ```sql

   ```
