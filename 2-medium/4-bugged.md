## Who are the top 10 authors by number of reviews?
 
Using bootcamp.books, find the top 10 authors by reviews, no_of_reviews is a string column with bad data, try your best to get the values to parse correctly

### These are the tables to query for this question:
**bootcamp.books**
- s_no int
- price double
- ranks int
- title string
- no_of_reviews string
- ratings string
- author string
- cover_type string
- year string
- genre string
### Your answer should include these columns:
- author varchar
- number_of_reviews bigint

## Answer
```sql
-- This question is bugged as of 2025-09-21

WITH A AS (
  SELECT 
    author,
    CAST(REGEXP_REPLACE(no_of_reviews, '[^0-9]', '') AS BIGINT) AS no_of_reviews 
  FROM bootcamp.books
)
SELECT
  author,
  SUM(no_of_reviews) AS number_of_reviews
FROM A
GROUP BY author
ORDER BY number_of_reviews DESC
LIMIT 10
```