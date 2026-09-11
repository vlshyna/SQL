Useful Links:
- [DataLemur Tutorial](https://datalemur.com/sql-tutorial/advanced-sql-tutorial-intro)
- [Ultimate SQL Interview Guide For Data Scientists & Data Analysts](https://datalemur.com/blog/sql-interview-guide#practice-take-home-sql-interview-challenges)
- [SQL Formatter](https://www.dpriver.com/pp/sqlformat.htm)

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

1) []()
   ```sql

   ```

1) []()
   ```sql

   ```
