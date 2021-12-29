[🏠HOME](README.md)

# How to Access SQL Using Pandas

---

## Connect
+ for general
```python
# pip install sqlalchemy
# pip install pymysql
from sqlalchemy import create_engine
# 初始化数据库连接，使用pymysql模块
# MySQL的用户：root, 密码:147369, 端口：3306,数据库：mydb
engine = create_engine('mysql+pymysql://root:147369@localhost:3306/mydb')
# df = pd.read_sql("select * from example_table", engine)
# or
# df = pd.read_sql("example_table", engine)
```
+ for `sqlite3`
```python
import sqlite3
conn = sqlite3.connect("example.db")
# df = pd.read_sql("select * from example_table", conn)
```

## Read
`pandas.read_sql(sql, con, index_col=None, coerce_float=True, params=None, parse_dates=None, columns=None, chunksize=None)`

[link to read_sql](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_sql.html)

## Write
`DataFrame.to_sql(name, con, schema=None, if_exists='fail', index=True, index_label=None, chunksize=None, dtype=None, method=None)[source]`

[link to to_sql](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_sql.html)
