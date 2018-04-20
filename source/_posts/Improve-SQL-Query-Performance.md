---
title: Improve SQL Query Performance
date: 2016-11-03 16:34:46
tags: [SQL]
categories: [Tools, SQL]
---

![](http://og2api1gp.bkt.clouddn.com/static/images/mysql.png "Optional title")

In general computer system, hard-drive read operations are about ten times more than write operation and in most cases, there are no performance issues with insert operation. The problems and bottlenecks are always detected in select queries.

![Alt text](http://og2api1gp.bkt.clouddn.com/static/images/hardware-delay.png "Optional title")

#### In this page, we summarize few different methods to improve SQL query performance.

1. Avoid * in SELECT statement. Give the name of columns which you require.

2. Avoid nchar and nvarchar if possible since both the data types takes just double memory as char and varchar.

3. Avoid NULL in fixed-length field. In case of requirement of NULL, use variable-length (varchar) field that takes less space for NULL.

4. Create Clustered and Non-Clustered Indexes.

5. Most selective columns should be placed leftmost in the key of a non-clustered index.

6. Better to create indexes on columns that have integer values instead of characters. Integer values use less overhead than character values.

7. Use joins instead of sub-queries.

8. Use Stored Procedure for frequently used data and more complex queries.

9. Keep transaction as small as possible since transaction lock the processing tables data and may results into deadlocks.

10. Avoid prefix “sp_” with user defined stored procedure name because SQL server first search the user defined procedure in the master database and after that in the current session database.

