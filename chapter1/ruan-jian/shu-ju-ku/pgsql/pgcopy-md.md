
---

[参考](http://bonesmoses.org/2014/07/25/friends-dont-let-friends-use-loops/)

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



