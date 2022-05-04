Nested queries are hard to read.

```SQL
SELECT  data_value_1
       ,data_value_2
FROM
(
	SELECT  data_value_1
	       ,COUNT(a) AS data_value_2
	FROM data_table
	GROUP BY  data_value_1
)
WHERE data_value_2 > 5
```

You can use Common Table Expressions to re-order the select-where sections around the nested query using the `WITH` keyword:

```SQL
WITH table_a AS
(
	SELECT  data_value_1
	       ,COUNT(a) AS data_value_2
	FROM data_table
	GROUP BY  data_value_1
)
SELECT  data_value_1
       ,data_value_2
FROM table_a
WHERE data_value_2 > 5
```
