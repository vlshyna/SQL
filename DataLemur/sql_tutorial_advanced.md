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


1) []()
   ```sql

   ```
