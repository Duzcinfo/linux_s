# pgsql

* 版本 ： postgrsql 11.4

如果用test\_db这个用户去直接创建`pg_pathman`,`pg_trgm`,会报权限的错误。

```text
错误: 创建扩展 "pg_trgm" 权限不够
```

* 解决办法

```sql
psql test_db -c'CREATE EXTENSION pg_pathman ;' # 为test_db创建pg_pathman这个扩展。

psql test_db -c'CREATE EXTENSION pg_rgm ;' # 为test_db创建pg_ptrgm这个扩展。
```

* 查看是否成功

```sql
psql -U test_db -h 192.168.50.41
\dx;
test_db=> \dx;
List of installed extensions

Name | Version | Schema | Description

------------+---------+------------+-------------------------------------------------------------------

pg_pathman | 1.5 | public | Partitioning tool for PostgreSQL

pg_trgm | 1.4 | public | text similarity measurement and index searching based on trigrams

plpgsql | 1.0 | pg_catalog | PL/pgSQL procedural language

(3 rows)
```

