# PG\_copy.md

[参考](http://bonesmoses.org/2014/07/25/friends-dont-let-friends-use-loops/)

## 导出 csv

**注意**：  
1. copy命令必须在plsql命令行执行，执行用户必须为superuser。  
2. 普通用户进行执行，需要在copy前面加入 “\”。

* 导出 csv

  pgsql 的 `COPY TO` 可以做这个事情，熟读非常快。

  ```sql
  COPY products
  TO '/path/to/output.csv'
  WITH csv;
  ```

* 可以直接指定属性

```sql
COPY products (name, price)
TO '/path/to/output.csv'
WITH csv;
```

* 也可以配合查询语句

```sql
COPY (
  SELECT name, category_name
  FROM products
  LEFT JOIN categories ON categories.id = products.category_id
)
TO '/path/to/output.csv'
WITH csv;
```

## 导入 csv

* 导入

```sql
COPY products
FROM '/path/to/input.csv'
WITH csv;
```

## python 导入

```python
import psycopg2

db_conn = psycopg2.connect(database = 'postgres', user = 'postgres')
cur = db_conn.cursor()

cur.execute(
  """PREPARE log_add AS
     INSERT INTO sensor_log (location, reading, reading_date)
     VALUES ($1, $2, $3);"""
)

file_input = open('/tmp/input.csv', 'r')
for line in file_input:
    cur.execute("EXECUTE log_add(%s, %s, %s)", line.strip().split(','))
file_input.close()

cur.execute("DEALLOCATE log_add");

db_conn.commit()
db_conn.close()
```

