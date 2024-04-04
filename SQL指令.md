主要查询
# 打死也要记住法则1：col

# 打死也要记住法则2：select

`SELECT` col,col,col 找什么？

`FROM` table 从哪找？

`WHERE` col 条件 条件是啥？

# 条件：数字(where)

`当查找条件col是数字`

`select * from table where col = 1`;

|Operator|Condition|SQL Example|解释|
|---|:-:|--:|---|
|=, !=, < ,<=, >, >=|Standard numerical operators|col != 4|等于 大于 小于|
|BETWEEN … AND …|Number is within range of two values (inclusive)|col BETWEEN 1.5 AND 10.5|在 X 和 X之间|
|NOT BETWEEN … AND …|Number is not within range of two values (inclusive)|co NOT BETWEEN 1 AND10|不在 X 和 X之间|
|IN (…)|Number exists in a list|col IN (2, 4, 6)|在 X 集合|
|NOT IN (…)|Number does not exist in a list|col NOT IN (1, 3, 5)|不在 X 集合|

# 条件：文本(where)

`当查找条件col是文本`

`select * from table where col like '%jin'`;

|Operator|Condition|SQL Example|解释|
|---|:-:|--:|---|
|=|Case sensitive exact string comparison (notice the single equals)|col = "abc"|等于|
|!= or <>|Case sensitive exact string inequality comparison|col != "abcd"|不等于|
|LIKE|Case insensitive exact string comparison|col LIKE "ABC"|等于|
|NOT LIKE|Case insensitive exact string inequality comparison|col NOT LIKE "ABCD"|不等于|
|%|Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE)|col LIKE "%AT%" (matches "AT", "ATTIC", "CAT" or even "BATS")|模糊匹配|
|_|Used anywhere in a string to match a single character (only with LIKE or NOT LIKE)|col LIKE "AN_" (matches "AND", but not "AN")|模糊匹配单字符|
|IN (…)|String exists in a list|col IN ("A", "B", "C")|在集合|
|NOT IN (…)|String does not exist in a list|co NOT IN ("D", "E", "F")|不在集合|

# 排序(rows)

`需要对结果rows排序和筛选部分rows`

`select * from table where col > 1 order by col asc limit 2 offset 2`

|Operator|Condition|SQL Example|解释|
|---|:-:|--:|---|
|ORDER BY|.|ORDER BY col ASC/DESC|按col排序|
|ASC|.|ORDER BY col ASC/DESC|升序|
|DESC|.|ORDER BY col ASC/DESC|降序|
|LIMIT OFFSET|.|LIMIT num_limit OFFSET num_offset|从offset取limit|
|ORDER BY|.|ORDER BY col1 ASC,col2 DESC|多列排序|

# join:连表(table)

`当查找的数据在多张关联table里`

`select * from table1 left join table2 on table1.id = table2.id where col > 1`

|Operator|Condition|SQL Example|解释|
|---|:-:|--:|---|
|JOIN .. ON ..|.|t1 JOIN t2 ON t1.id = t2.id|按ID连成1个表|
|INNER JOIN|.|t1 INNER JOIN t2 ON t1.id = t2.id|只保留id相等的row|
|LEFT JOIN|.|t1 LEFT JOIN t2 ON t1.id = t2.id|保留t1的所有row|
|RIGHT JOIN|.|t1 RIGHT JOIN t2 ON t1.id = t2.id|保留t2的所有row|
|IS/IS NOT NULL|.|col IS/IS NOT NULL|col是不是为null|

# 算式(select / where)

`当需要对select的col 或 where条件的col 经过一定计算后才能使用`

`select *,col*2 from table where col/2 > 1`

|Operator|Condition|SQL Example|解释|
|---|:-:|--:|---|
|+ - * / %|.|col1 + col2|col加减乘除|
|substr|.|substr(col,0,4)|字符串截取|
|AS|.|col * 2 AS col_new|col取别名|
|...|||还有很多|

# 统计（select）

`对查找的rows需要按col分组统计的情况`

`select count(*),avg(col),col from table where col > 1 group by col`

|Operator|Condition|SQL Example|解释|
|---|:-:|--:|---|
|COUNT(*), COUNT(column)|A common function used to counts the number of rows in the group if no column name is specified. Otherwise, count the number of rows in the group with non-NULL values in the specified column.|count(col)|计数|
|MIN(column)|Finds the smallest numerical value in the specified column for all rows in the group.|min(col)|最小|
|MAX(column)|Finds the largest numerical value in the specified column for all rows in the group.|max(col)|最大|
|AVG(column)|Finds the average numerical value in the specified column for all rows in the group.|avg(col)|平均|
|SUM(column)|Finds the sum of all numerical values in the specified column for the rows in the group.|sum(col)|求和|
|GROUP BY|.|group by col,col2|分组|
|HAVING|.|HAVING col>100|分组后条件|

# 子表 (table)

`一次select的结果rows作为下一次select的临时table才能得到最终结果`

`select * from (select * from table where col > 1) as tmp where col < 1`

|Operator|Condition|SQL Example|解释|
|---|:-:|--:|---|
|（select -）as tmp||（select -）as tmp|select结果做子表|
|in（select -）||in（select -）|select结果做条件|
|avg（select -）||avg（select -）|select结果做条件|