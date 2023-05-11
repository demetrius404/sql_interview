## Task 2
Найти второй по продажам магазин

|id|name |sold_total|
|--|-----|----------|
|1 |shop1|10        |
|2 |shop2|12        |
|3 |shop3|14        |
|4 |shop3|1         |
|5 |shop2|12        |
|6 |shop1|11        |

## SQL
```sql
DROP TABLE IF EXISTS tab;

CREATE TABLE tab (
id INTEGER,
name VARCHAR,
sold_total INTEGER
);

INSERT INTO tab VALUES 
(1, 'shop1', 10),
(2, 'shop2', 12),
(3, 'shop3', 14),
(4, 'shop3', 1),
(5, 'shop2', 12),
(6, 'shop1', 11);

SELECT * FROM tab;
```

|id|name |sold_total|
|--|-----|----------|
|1 |shop1|10        |
|2 |shop2|12        |
|3 |shop3|14        |
|4 |shop3|1         |
|5 |shop2|12        |
|6 |shop1|11        |

```sql
SELECT
name,
sum(sold_total) as sum_sold_total,
dense_rank() OVER (ORDER BY sum(sold_total) DESC) AS r
FROM tab
GROUP BY name
ORDER BY sum_sold_total DESC;
```

|name |sum_sold_total|r|
|-----|--------------|-|
|shop2|24            |1|
|shop1|21            |2|
|shop3|15            |3|
```sql
SELECT '--- SOLUTION ---';

WITH T AS
(
  SELECT
  name,
  dense_rank() OVER (ORDER BY sum(sold_total) DESC) AS r
  FROM tab
  GROUP BY name
)
SELECT 
name
FROM T
WHERE r=2;
```

|name |
|-----|
|shop1|
