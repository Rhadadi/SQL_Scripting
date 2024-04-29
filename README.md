# SQL Scripting Variations

| Feature | Presto (Trino) | Oracle SQL | Amazon Redshift | Netezza | PostgreSQL |
|---|---|---|---|---|---|
| Limiting results | `LIMIT n` clause | `FETCH FIRST n ROWS ONLY` or `ROWNUM <= n` | `LIMIT n` clause | `LIMIT n` clause | `LIMIT n` clause |
| Joining tables | Supports ANSI SQL joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN` | Supports ANSI SQL joins and legacy `(+)` syntax for outer joins | Supports ANSI SQL joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN` | Supports ANSI SQL joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN` | Supports ANSI SQL joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN` |
| Subqueries | Supports `WITH` clause for Common Table Expressions (CTEs) | Supports `WITH` clause for CTEs, `START WITH` and `CONNECT BY` clauses for hierarchical queries | Supports `WITH` clause for CTEs | Supports `WITH` clause for CTEs | Supports `WITH` clause for CTEs |
| Date functions | `date_trunc('day', timestamp)` for date truncation | `TRUNC(date, 'fmt')` for date truncation, `TO_DATE(string, 'fmt')` for parsing dates | `DATE_TRUNC('day', timestamp)` for date truncation, `TO_DATE(string, 'fmt')` for parsing dates | `DATE_TRUNC('day', timestamp)` for date truncation, `TO_DATE(string, 'fmt')` for parsing dates | `date_trunc('day', timestamp)` for date truncation, `TO_TIMESTAMP(string, 'fmt')` for parsing dates |
| String functions | `CONCAT(col1, col2)` or `\|\|` operator for concatenation | `CONCAT(col1, col2)` or `\|\|` operator for concatenation | `CONCAT(col1, col2)` or `\|\|` operator for concatenation | `CONCAT(col1, col2)` or `\|\|` operator for concatenation | `CONCAT(col1, col2)` or `\|\|` operator for concatenation |
| Conditional expressions | `CASE WHEN condition THEN value END` syntax | `CASE` expressions and `DECODE` function for conditional logic | `CASE WHEN condition THEN value END` syntax | `CASE WHEN condition THEN value END` syntax | `CASE WHEN condition THEN value END` syntax |
| Temporary tables | `CREATE TEMPORARY TABLE` for session-scoped temporary tables | `CREATE GLOBAL TEMPORARY TABLE` for session or transaction-scoped temporary tables | `CREATE TEMPORARY TABLE` for session-scoped temporary tables | `CREATE TEMPORARY TABLE` for session-scoped temporary tables | `CREATE TEMPORARY TABLE` for session-scoped temporary tables |
| Set operations | Supports `UNION`, `INTERSECT`, and `EXCEPT` operators | Supports `UNION`, `INTERSECT`, and `MINUS` operators | Supports `UNION`, `INTERSECT`, and `EXCEPT` operators | Supports `UNION`, `INTERSECT`, and `EXCEPT` operators | Supports `UNION`, `INTERSECT`, and `EXCEPT` operators |
| Analytic functions | Supports `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` functions | Supports a wide range of analytic functions, including `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`, `FIRST_VALUE()`, `LAST_VALUE()`, etc. | Supports `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` functions | Supports `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` functions | Supports `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`, `FIRST_VALUE()`, `LAST_VALUE()` functions |
| Pivot and unpivot | Requires custom queries using conditional aggregation | Supports `PIVOT` and `UNPIVOT` operators for row-to-column and column-to-row transformations | Requires custom queries using conditional aggregation | Requires custom queries using conditional aggregation | Requires custom queries using conditional aggregation or the `crosstab` function from the `tablefunc` extension |
| JSON functions | Supports `JSON_EXTRACT()` and `JSON_PARSE()` functions | Supports `JSON_VALUE()`, `JSON_QUERY()`, and `JSON_TABLE()` functions for parsing and manipulating JSON data | Supports `JSON_EXTRACT_PATH_TEXT()` and other JSON functions | Limited JSON support | Extensive JSON support with functions and operators like `->`, `->>`, `@>`, `?`, `jsonb_set()`, etc. |
| Regular expressions | Supports `REGEXP_LIKE(col, pattern)` function | Supports `REGEXP_LIKE(col, pattern)`, `REGEXP_SUBSTR()`, `REGEXP_INSTR()`, `REGEXP_REPLACE()` functions | Supports `REGEXP_INSTR(col, pattern)`, `REGEXP_SUBSTR()`, `REGEXP_COUNT()` functions | Supports `REGEXP_LIKE(col, pattern)`, `REGEXP_SUBSTR(col, pattern)` functions | Extensive support for regular expressions with functions and operators like `~`, `~*`, `regexp_match()`, `regexp_replace()`, etc. |
| Partitioning | Connector-based, supports Hive-style partitioning | Native support for range, list, and hash partitioning | Native support for range, list, and hash partitioning | Supports Netezza's proprietary data distribution and data slice partitioning | Native support for range, list, and hash partitioning using declarative partitioning syntax |
| Indexes | Utilizes indexes of the underlying data stores | Supports various index types, including B-tree, bitmap, function-based indexes, etc. | Supports compound and interleaved indexes | Supports Netezza's zone maps and clustering | Supports various index types, including B-tree, GIN, GiST, SP-GiST, BRIN, hash indexes, etc. |
| Stored Procedures | Not supported | Supports stored procedures using PL/SQL | Supports stored procedures using SQL and Python | Supports stored procedures using NZPLSQL | Supports stored procedures using PL/pgSQL, SQL, and other languages |
| Transactions | Read-only transactions for most connectors | Full ACID transaction support | Full ACID transaction support | Full ACID transaction support | Full ACID transaction support |
| Sequence objects | Not supported | Supports `SEQUENCE` objects for generating unique sequential values | Supports `SEQUENCE` objects for generating unique sequential values | Supports `GENERATE_UNIQUE()` and `GENERATE_SERIES()` functions for generating unique sequential values | Supports `SERIAL` data type and `SEQUENCE` objects for generating unique sequential values |
| Recursive queries | Not supported | Supports recursive queries using `CONNECT BY` clause | Supports recursive queries using recursive Common Table Expressions (CTEs) | Supports recursive queries using recursive Common Table Expressions (CTEs) | Supports recursive queries using recursive Common Table Expressions (CTEs) |
| Full-text search | Not supported | Supports full-text search using Oracle Text | Not natively supported, requires external tools like Elasticsearch | Not supported | Supports full-text search using built-in capabilities like `to_tsvector()`, `to_tsquery()`, `@@` operator, etc. |
| Spatial data types and functions | Not natively supported | Supports spatial data types and functions using Oracle Spatial | Supports spatial data types and functions using the PostGIS extension | Not supported | Supports spatial data types and functions using the PostGIS extension |
| Autonomous transactions | Not supported | Supports autonomous transactions using `AUTONOMOUS_TRANSACTION` pragma | Not supported | Not supported | Not supported |
| Missing value handling | `NULL` represents missing data, comparison with `NULL` returns `NULL` | `NULL` represents missing data, comparison with `NULL` returns `NULL` | `NULL` represents missing data, comparison with `NULL` returns `UNKNOWN` (neither true nor false) | `NULL` represents missing data, comparison with `NULL` returns `NULL` or `UNKNOWN` depending on the operator | `NULL` represents missing data, comparison with `NULL` returns `NULL` or `UNKNOWN` depending on the operator, supports `IS [NOT] DISTINCT FROM` for non-null comparison |
| Data types | Supports standard SQL data types, with some Hive-specific types | Extensive support for data types, including Oracle-specific types like `VARCHAR2`, `NUMBER`, `CLOB`, `BLOB`, etc. | Supports standard SQL data types, with some Redshift-specific types like `SUPER` for semi-structured data | Supports standard SQL data types, with some Netezza-specific types | Extensive support for data types, including PostgreSQL-specific types like `ARRAY`, `HSTORE`, `JSONB`, etc. |
| Table sampling | Supports `TABLESAMPLE` operator for random sampling | Supports `SAMPLE` clause for random sampling | Supports `TABLESAMPLE` operator for random sampling | Supports `TABLESAMPLE` operator for random sampling | Supports `TABLESAMPLE` operator for random sampling |
| Materialized views | Not supported | Supports materialized views using `CREATE MATERIALIZED VIEW` statement | Supports materialized views using `CREATE MATERIALIZED VIEW` statement | Supports materialized views using `CREATE MATERIALIZED VIEW` statement | Supports materialized views using `CREATE MATERIALIZED VIEW` statement |
| Lateral joins | Supports lateral joins using `LATERAL` keyword | Supports lateral joins using `LATERAL` keyword | Supports lateral joins using `LATERAL` keyword | Not supported | Supports lateral joins using `LATERAL` keyword |
| Grouping sets, cube, rollup | Supports `GROUPING SETS`, `CUBE`, and `ROLLUP` operations | Supports `GROUPING SETS`, `CUBE`, and `ROLLUP` operations | Supports `GROUPING SETS`, `CUBE`, and `ROLLUP` operations | Supports `GROUPING SETS`, `CUBE`, and `ROLLUP` operations | Supports `GROUPING SETS`, `CUBE`, and `ROLLUP` operations |
