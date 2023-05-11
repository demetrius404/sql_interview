## Task 1

Удалить дубли одним запросом
Дана таблица вида
|id|name |address|
|--|-----|-------|
|1 |Marat|Moscow |
|2 |Anton|Moscow |
|3 |Anwar|Spb    |
|4 |Anton|Samara |

* Уточнение: В примере дубликатом считается строка с одинаковым `name`

## SQL
```sql
DROP TABLE IF EXISTS tab;

CREATE TABLE tab (
id INTEGER,
name VARCHAR,
address VARCHAR
);

INSERT INTO tab VALUES 
(1, 'Marat', 'Moscow'),
(2, 'Anton', 'Moscow'),
(3, 'Anwar', 'Spb'),
(4, 'Anton', 'Samara');

SELECT * FROM tab;
```
|id|name |address|
|--|-----|-------|
|1 |Marat|Moscow |
|2 |Anton|Moscow |
|3 |Anwar|Spb    |
|4 |Anton|Samara |

```sql
SELECT '--- SOLUTION ---';

DELETE FROM tab
WHERE id IN (
  SELECT 
  id
  FROM ( 
    SELECT 
    id,
    row_number() OVER (PARTITION BY name) AS n
    FROM tab
  ) WHERE n > 1
);

SELECT * FROM tab;
```

|id|name |address|
|--|-----|-------|
|1 |Marat|Moscow |
|2 |Anton|Moscow |
|3 |Anwar|Spb    |
