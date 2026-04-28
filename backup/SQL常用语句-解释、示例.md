下面给出「带中文解释 + 直接可复制」的 SQL 模板清单。  
每条语句都写成三段：  
① 作用说明（中文）  
② 完整模板（直接复制，把中文占位符换成实际对象名即可运行）  
③ 示例（可选，帮助你快速代入）

按使用频率由高到低排列，方便速查。

----------------  
1. 查询整张表  
【说明】一次性取出全部行和列，仅适合小表。  
模板：  
SELECT * FROM 表名;  
示例：  
SELECT * FROM user;

----------------  
2. 查询指定列  
【说明】只取需要的列，减少网络 IO。  
模板：  
SELECT 列1, 列2 FROM 表名;  
示例：  
SELECT id, name FROM user;

----------------  
3. 条件过滤  
【说明】按 WHERE 子句过滤，避免全表扫描。  
模板：  
SELECT * FROM 表名 WHERE 条件;  
示例：  
SELECT * FROM user WHERE age > 18;

----------------  
4. 模糊搜索（左前缀）  
【说明】模糊匹配以某字符串开头。% 表示任意长度。  
模板：  
SELECT * FROM 表名 WHERE 列 LIKE '前缀%';  
示例：  
SELECT * FROM user WHERE name LIKE '张%';

----------------  
5. 排序 + 取前 N 条  
【说明】先排序再 LIMIT，常用于排行榜、最新记录。  
模板：  
SELECT * FROM 表名 ORDER BY 列 DESC LIMIT N;  
示例：  
SELECT * FROM order ORDER BY create_time DESC LIMIT 10;

----------------  
6. 去重查询  
【说明】返回唯一值列表，通常用于维度列。  
模板：  
SELECT DISTINCT 列 FROM 表名;  
示例：  
SELECT DISTINCT department FROM employee;

----------------  
7. 计数  
【说明】统计行数，常配合 WHERE 做条件计数。  
模板：  
SELECT COUNT(*) FROM 表名 WHERE 条件;  
示例：  
SELECT COUNT(*) FROM user WHERE status = 1;

----------------  
8. 分组汇总  
【说明】GROUP BY + 聚合函数，实现“每组的统计值”。  
模板：  
SELECT 分组列, COUNT(*) AS 数量 FROM 表名 GROUP BY 分组列;  
示例：  
SELECT department, COUNT(*) AS emp_cnt FROM employee GROUP BY department;

----------------  
9. 分组后二次过滤  
【说明】GROUP BY 后再用 HAVING 筛掉不满足条件的组。  
模板：  
SELECT 分组列, COUNT(*) AS 数量  
FROM 表名  
GROUP BY 分组列  
HAVING COUNT(*) > 阈值;  
示例：  
SELECT department, COUNT(*) AS emp_cnt  
FROM employee  
GROUP BY department  
HAVING emp_cnt > 5;

----------------  
10. 求和 / 平均 / 最大 / 最小  
【说明】聚合函数一次性计算。  
模板：  
SELECT  
  SUM(数值列) AS 总和,  
  AVG(数值列) AS 平均,  
  MAX(数值列) AS 最大,  
  MIN(数值列) AS 最小  
FROM 表名  
WHERE 条件;  
示例：  
SELECT SUM(amount), AVG(amount) FROM order WHERE create_date = CURDATE();

----------------  
11. 插入单行  
【说明】指定列插入一条记录，自动增长列可省略。  
模板：  
INSERT INTO 表名 (列1, 列2) VALUES (值1, 值2);  
示例：  
INSERT INTO user (name, age) VALUES ('张三', 25);

----------------  
12. 批量插入  
【说明】一次提交多行，减少网络往返。  
模板：  
INSERT INTO 表名 (列1, 列2) VALUES  
(值1, 值2),  
(值3, 值4),  
(值5, 值6);  
示例：  
INSERT INTO user (name, age) VALUES ('李四', 30), ('王五', 28);

----------------  
13. 更新数据  
【说明】务必带 WHERE，否则整表被改。  
模板：  
UPDATE 表名 SET 列1 = 新值1, 列2 = 新值2 WHERE 条件;  
示例：  
UPDATE user SET age = 26 WHERE id = 1001;

----------------  
14. 删除数据  
【说明】务必带 WHERE，否则整表被删。  
模板：  
DELETE FROM 表名 WHERE 条件;  
示例：  
DELETE FROM user WHERE status = 0;

----------------  
15. 创建表  
【说明】定义列、主键、常见约束。  
模板：  
CREATE TABLE 表名 (  
  id INT PRIMARY KEY AUTO_INCREMENT,  
  列2 数据类型 NOT NULL,  
  列3 数据类型 DEFAULT 默认值,  
  索引列1, 索引列2  
);  
示例：  
CREATE TABLE user (  
  id INT PRIMARY KEY AUTO_INCREMENT,  
  name VARCHAR(50) NOT NULL,  
  age INT DEFAULT 0,  
  INDEX idx_name (name)  
);

----------------  
16. 给表加索引  
【说明】加速 WHERE / JOIN / ORDER BY 列。  
模板：  
CREATE INDEX 索引名 ON 表名 (列);  
示例：  
CREATE INDEX idx_user_age ON user (age);

----------------  
17. 两表内连接  
【说明】只保留两表匹配成功的行。  
模板：  
SELECT a.*, b.*  
FROM 表A a  
INNER JOIN 表B b ON a.关联列 = b.关联列  
WHERE a.条件;  
示例：  
SELECT u.*, o.amount  
FROM user u  
INNER JOIN orders o ON u.id = o.user_id  
WHERE u.status = 1;

----------------  
18. 左连接（保留左表全部）  
模板：  
SELECT a.*, b.*  
FROM 表A a  
LEFT JOIN 表B b ON a.关联列 = b.关联列;  
示例：  
SELECT u.*, o.amount  
FROM user u  
LEFT JOIN orders o ON u.id = o.user_id;

----------------  
19. 子查询（IN）  
【说明】某列值存在于子查询结果中。  
模板：  
SELECT * FROM 表名 WHERE 列 IN (SELECT 列 FROM 其他表 WHERE 条件);  
示例：  
SELECT * FROM user WHERE id IN (SELECT user_id FROM orders WHERE amount > 1000);

----------------  
20. 事务范例  
【说明】多条 SQL 原子提交。  
模板：  
BEGIN;  
  UPDATE 账户表 SET 余额 = 余额 - 100 WHERE id = 1;  
  UPDATE 账户表 SET 余额 = 余额 + 100 WHERE id = 2;  
COMMIT;  
-- 出错时执行 ROLLBACK;

----------------  
21. 备份 & 恢复（命令行）  
【说明】mysqldump 逻辑备份，跨平台通用。  
备份：  
mysqldump -u 用户名 -p 数据库名 > 备份文件.sql  
恢复：  
mysql -u 用户名 -p 数据库名 < 备份文件.sql

----------------  
22. 查看表结构  
模板：  
DESCRIBE 表名;  
示例：  
DESCRIBE user;

----------------  
23. 查看当前连接  
模板：  
SHOW PROCESSLIST;

----------------  
24. 查数据库占用大小  
模板：  
SELECT  
  table_schema AS '数据库',  
  ROUND(SUM(data_length + index_length)/1024/1024, 2) AS '大小(MB)'  
FROM information_schema.TABLES  
GROUP BY table_schema;

----------------  
25. 取前 N 条 / 最后 N 条  
【说明】ORDER BY + LIMIT 的经典用法。  
前 N 条：  
SELECT * FROM 表名 ORDER BY 主键 ASC LIMIT N;  
最后 N 条：  
SELECT * FROM 表名 ORDER BY 主键 DESC LIMIT N;

----------------  
使用方式：  
1. 先读「作用说明」确认需求；  
2. 复制「模板」到 SQL 客户端；  
3. 替换中文占位符（表名、列名、条件、值）即可执行。