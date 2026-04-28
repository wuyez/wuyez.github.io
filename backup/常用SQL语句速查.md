**全文摘要**
常用SQL语句速查

**关键段落**

*   **基本查询语句**

    *   查询所有数据：`SELECT * FROM 表名;`

    *   查询特定列：`SELECT 列名1, 列名2 FROM 表名;`

    *   条件查询：`SELECT * FROM 表名 WHERE 条件;`

    *   模糊查询：`SELECT * FROM 表名 WHERE 列名 LIKE '模式%';`

    *   排序查询：`SELECT * FROM 表名 ORDER BY 列名 ASC|DESC;`

    *   限制返回行数：`SELECT * FROM 表名 LIMIT 10;`

    *   去重查询：`SELECT DISTINCT 列名 FROM 表名;`

*   **聚合与分组**

    *   聚合函数 - 计数：`SELECT COUNT(*) FROM 表名;`

    *   分组查询：`SELECT 列名, COUNT(*) FROM 表名 GROUP BY 列名;`

    *   条件分组：`SELECT 列名, COUNT(*) FROM 表名 GROUP BY 列名 HAVING COUNT(*) > 1;`

    *   计算总和：`SELECT SUM(列名) FROM 表名;`

    *   计算平均值：`SELECT AVG(列名) FROM 表名;`

    *   计算最大值：`SELECT MAX(列名) FROM 表名;`

    *   计算最小值：`SELECT MIN(列名) FROM 表名;`

*   **数据操作**

    *   插入数据：`INSERT INTO 表名 (列名1, 列名2) VALUES (值1, 值2);`

    *   批量插入数据：`INSERT INTO 表名 (列名1, 列名2) VALUES (值1, 值2), (值3, 值4);`

    *   更新数据：`UPDATE 表名 SET 列名 = 新值 WHERE 条件;`

    *   删除数据：`DELETE FROM 表名 WHERE 条件;`

*   **表操作**

    *   创建表：`CREATE TABLE 表名 (列名1 数据类型, 列名2 数据类型);`

    *   删除表：`DROP TABLE 表名;`

    *   修改表结构：`ALTER TABLE 表名 ADD 列名 数据类型;`

    *   删除表中的列：`ALTER TABLE 表名 DROP COLUMN 列名;`

    *   重命名表：`ALTER TABLE 旧表名 RENAME TO 新表名;`

*   **索引与视图**

    *   创建索引：`CREATE INDEX 索引名 ON 表名 (列名);`

    *   删除索引：`DROP INDEX 索引名;`

    *   创建视图：`CREATE VIEW 视图名 AS SELECT * FROM 表名;`

    *   删除视图：`DROP VIEW 视图名;`

*   **连接查询**

    *   内连接：`SELECT * FROM 表1 INNER JOIN 表2 ON 表1.列名 = 表2.列名;`

    *   左连接：`SELECT * FROM 表1 LEFT JOIN 表2 ON 表1.列名 = 表2.列名;`

    *   右连接：`SELECT * FROM 表1 RIGHT JOIN 表2 ON 表1.列名 = 表2.列名;`

    *   全连接：`SELECT * FROM 表1 FULL OUTER JOIN 表2 ON 表1.列名 = 表2.列名;`

*   **子查询与集合**

    *   子查询：`SELECT * FROM 表名 WHERE 列名 IN (SELECT 列名 FROM 其他表名);`

    *   存在查询：`SELECT * FROM 表名 WHERE EXISTS (SELECT 1 FROM 其他表名 WHERE 条件);`

    *   联合查询：`SELECT 列名 FROM 表1 UNION SELECT 列名 FROM 表2;`

*   **日期与时间**

    *   获取当前时间：`SELECT NOW();`

    *   获取当前日期：`SELECT CURDATE();`

    *   日期加法：`SELECT DATE_ADD(日期, INTERVAL 1 DAY);`

    *   日期减法：`SELECT DATE_SUB(日期, INTERVAL 1 DAY);`

    *   格式化日期：`SELECT DATE_FORMAT(日期, '%Y-%m-%d');`

*   **字符串处理**

    *   字符串连接：`SELECT CONCAT(列名1, 列名2) FROM 表名;`

    *   字符串长度：`SELECT LENGTH(列名) FROM 表名;`

    *   字符串截取：`SELECT SUBSTRING(列名, 1, 5) FROM 表名;`

    *   查找字符串位置：`SELECT LOCATE('子串', 列名) FROM 表名;`

    *   大写转换：`SELECT UPPER(列名) FROM 表名;`

    *   小写转换：`SELECT LOWER(列名) FROM 表名;`

    *   去除空格：`SELECT TRIM(列名) FROM 表名;`

*   **其他高级功能**

    *   使用CASE语句：`SELECT 列名, CASE WHEN 条件 THEN '值1' ELSE '值2' END FROM 表名;`

    *   使用IF语句：`SELECT 列名, IF(条件, '值1', '值2') FROM 表名;`

    *   使用COALESCE函数：`SELECT COALESCE(列名, '默认值') FROM 表名;`

    *   使用NULLIF函数：`SELECT NULLIF(列名1, 列名2) FROM 表名;`

    *   获取唯一值的数量：`SELECT COUNT(DISTINCT 列名) FROM 表名;`

    *   使用GROUP\_CONCAT：`SELECT GROUP_CONCAT(列名) FROM 表名 GROUP BY 其他列名;`

*   **事务管理**

    *   事务开始：`BEGIN;`

    *   提交事务：`COMMIT;`

    *   回滚事务：`ROLLBACK;`

*   **游标与存储过程**

    *   创建游标：`DECLARE 游标名 CURSOR FOR SELECT 列名 FROM 表名;`

    *   打开游标：`OPEN 游标名;`

    *   获取游标数据：`FETCH 游标名 INTO 变量名;`

    *   关闭游标：`CLOSE 游标名;`

    *   创建存储过程：`CREATE PROCEDURE 存储过程名 AS BEGIN ... END;`

    *   调用存储过程：`CALL 存储过程名();`

*   **函数与触发器**

    *   创建函数：`CREATE FUNCTION 函数名() RETURNS 数据类型 AS BEGIN ... END;`

    *   调用函数：`SELECT 函数名();`

    *   创建触发器：`CREATE TRIGGER 触发器名 BEFORE INSERT ON 表名 FOR EACH ROW SET 新列 = '值';`

    *   删除触发器：`DROP TRIGGER 触发器名;`

*   **系统信息查询**

    *   查询当前用户：`SELECT CURRENT_USER();`

    *   查询当前数据库：`SELECT DATABASE();`

    *   查询表的行数和大小：`SELECT TABLE_NAME, TABLE_ROWS, DATA_LENGTH FROM information_schema.TABLES WHERE TABLE_SCHEMA = '数据库名';`

    *   获取表的创建时间：`SELECT CREATE_TIME FROM information_schema.TABLES WHERE TABLE_NAME = '表名';`

    *   获取表的修改时间：`SELECT UPDATE_TIME FROM information_schema.TABLES WHERE TABLE_NAME = '表名';`

*   **其他实用查询**

    *   使用LIMIT与ORDER BY结合：`SELECT * FROM 表名 ORDER BY 列名 LIMIT 10;`

    *   查询表的外键约束：`SELECT CONSTRAINT_NAME, TABLE_NAME FROM information_schema.KEY_COLUMN_USAGE WHERE TABLE_SCHEMA = '数据库名';`

    *   查询表的主键约束：`SELECT CONSTRAINT_NAME, TABLE_NAME FROM information_schema.TABLE_CONSTRAINTS WHERE TABLE_SCHEMA = '数据库名' AND CONSTRAINT_TYPE = 'PRIMARY KEY';`

    *   使用ROLLUP进行分组汇总：`SELECT 列名, SUM(列名2) FROM 表名 GROUP BY 列名 WITH ROLLUP;`

    *   获取前N条记录：`SELECT * FROM 表名 LIMIT N;`

    *   获取最后N条记录：\`SELECT \* FROM 表
