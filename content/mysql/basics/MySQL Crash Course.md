# MySQL 基础使用：快速上手篇

日期：2025-06-07  
作者：SeraphimWei  
参考书籍：MySQL Crash Course（第 3 章）

---

## 登录数据库

```bash
mysql -u <username> -p<password> -P <port>
```
（1）

说明：
- `-u` 用户名
- `-p` 密码（注意不要有空格）
- `-P` 端口（默认 3306）

示例：

```bash
mysql -u root -p123456 -P 3306
```

---

## 退出 MySQL

```sql
QUIT;
-- 或
EXIT;
```
（2）

---

## 使用数据库

```sql
USE employees;
```
（3）

> 输出：Database changed

---

## 查看数据库

```sql
SHOW DATABASES;
```
（4）

| Database            |
|---------------------|
| information_schema  |
| mysql               |
| performance_schema  |
| sys                 |
| employees           |

---

## 查看数据表

```sql
SHOW TABLES;
```
（5）

| Tables_in_employees |
|---------------------|
| departments         |
| employees           |
| salaries            |
| titles              |

---

## 查看表结构

```sql
SHOW COLUMNS FROM employees;
-- 或
DESCRIBE employees;
```
（6）

| Field      | Type           | Null | Key | Default | Extra          |
|------------|----------------|------|-----|---------|----------------|
| emp_no     | int            | NO   | PRI | NULL    | auto_increment |
| birth_date | date           | NO   |     | NULL    |                |
| first_name | varchar(14)    | NO   |     | NULL    |                |
| last_name  | varchar(16)    | NO   |     | NULL    |                |
| gender     | enum('M','F')  | NO   |     | NULL    |                |
| hire_date  | date           | NO   |     | NULL    |                |

---

## 查看服务器状态

```sql
SHOW STATUS;
```
（7）

| Variable_name     | Value   |
|-------------------|---------|
| Aborted_clients   | 0       |
| Threads_connected | 3       |
| Uptime            | 4523    |
| ...               | ...     |

---

## 查看当前用户权限

```sql
SHOW GRANTS;
```
（8）

| Grants for root@localhost                                                                  |
|---------------------------------------------------------------------------------------------|
| GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY PASSWORD '****' WITH GRANT OPTION |

---

## 查看错误与警告

```sql
SHOW ERRORS;
SHOW WARNINGS;
```
（9）

| Level | Code | Message                          |
|-------|------|----------------------------------|
| Error | 1064 | You have an error in your syntax |

或：

| Level   | Code | Message                          |
|---------|------|----------------------------------|
| Warning | 1366 | Incorrect string value for 'xx'. |

---

# MySQL 基础使用：检索数据

日期：2025-06-07  
作者：SeraphimWei  
参考书籍：MySQL Crash Course（第 4 章）

---

## 基本 SELECT 查询

```sql
SELECT name
FROM students;
```
（1）

| name      |
|-----------|
| Alice     |
| Bob       |
| Charlie   |

---

## 查询多个列

```sql
SELECT name, age
FROM students;
```
（2）

| name    | age |
|---------|-----|
| Alice   | 20  |
| Bob     | 21  |
| Charlie | 22  |

---

## 查询所有列

```sql
SELECT *
FROM students;
```
（3）

| id | name    | age | grade |
|----|---------|-----|--------|
| 1  | Alice   | 20  | A      |
| 2  | Bob     | 21  | B      |
| 3  | Charlie | 22  | A      |

---

## 去重查询

```sql
SELECT DISTINCT grade
FROM students;
```
（4）

| grade |
|--------|
| A      |
| B      |

---

## 限制返回行数

```sql
SELECT name
FROM students
LIMIT 2;
```
（5）

| name    |
|---------|
| Alice   |
| Bob     |

---

## 分页查询

```sql
SELECT name
FROM students
LIMIT 1, 2;
```
（6）

说明：
- `LIMIT 1, 2`：跳过第 1 行，从第 2 行开始返回 2 行数据（行号从 0 开始）

| name    |
|---------|
| Bob     |
| Charlie |

---

# MySQL 基础使用：排序检索数据

日期：2025-06-07  
作者：SeraphimWei  
参考书籍：MySQL Crash Course（第 5 章）

---

## 按列排序（默认升序，A → Z）

```sql
SELECT name
FROM students
ORDER BY name;
```
（1）

| name    |
|---------|
| Alice   |
| Bob     |
| Charlie |

---

## 多列排序（按优先级排序）

```sql
SELECT name, grade
FROM students
ORDER BY grade, name;
```
（2）

| name    | grade |
|---------|--------|
| Alice   | A      |
| Charlie | A      |
| Bob     | B      |

---

## 降序排列

```sql
SELECT age
FROM students
ORDER BY age DESC;
```
（3）

| age |
|-----|
| 22  |
| 21  |
| 20  |

---

## 多列排序 + 降序优先

```sql
SELECT name, age
FROM students
ORDER BY age DESC, name;
```
（4）

| name    | age |
|---------|-----|
| Charlie | 22  |
| Bob     | 21  |
| Alice   | 20  |

---

## 明确指定升序

```sql
SELECT name
FROM students
ORDER BY name ASC;
```
（5）

| name    |
|---------|
| Alice   |
| Bob     |
| Charlie |

---

## 查找最大值（结合 LIMIT）

```sql
SELECT age
FROM students
ORDER BY age DESC
LIMIT 1;
```
（6）

| age |
|-----|
| 22  |

---

# MySQL 基础使用：过滤数据

日期：2025-06-07  
作者：SeraphimWei  
参考书籍：MySQL Crash Course（第 6 章）

---

## 基本 WHERE 查询

```sql
SELECT c1, c2
FROM table_name
WHERE c2 = n;
```
（1）

---

## WHERE 和 ORDER BY 的执行顺序

- SQL 执行顺序：先执行 `WHERE` 进行过滤，再执行 `ORDER BY` 排序
- 原因：排序必须在筛选后的结果上进行，否则会影响排序逻辑和性能

---

## WHERE 子句支持的操作符

| 操作符             | 含义         | 示例                             |
|--------------------|--------------|----------------------------------|
| =                  | 等于         | `WHERE age = 18`                |
| <> 或 !=           | 不等于       | `WHERE status <> 'done'`       |
| <                  | 小于         | `WHERE score < 60`             |
| <=                 | 小于等于     | `WHERE score <= 60`            |
| >                  | 大于         | `WHERE salary > 10000`         |
| >=                 | 大于等于     | `WHERE age >= 30`              |
| BETWEEN a AND b    | 范围包含两端 | `WHERE age BETWEEN 18 AND 25`  |
| IS NULL / NOT NULL | NULL判断     | `WHERE phone IS NOT NULL`      |

（2）

---

## 字符串比较示例（默认不区分大小写）

```sql
SELECT name
FROM students
WHERE name = 'alice';
```
（3）

说明：默认情况下 MySQL 对字符串不区分大小写（除非使用 binary 或设置区分大小写的 collation）。

**示例返回：**

| name    |
|---------|
| Alice   |
| alice   |
| ALICE   |

---

## 数值比较示例（小于等于）

```sql
SELECT score
FROM exams
WHERE score <= 60;
```
（4）

**示例返回：**

| score |
|-------|
| 59    |
| 60    |
| 45    |

---

## BETWEEN 范围示例

```sql
SELECT age
FROM users
WHERE age BETWEEN 18 AND 30;
```
（5）

**示例返回：**

| age |
|-----|
| 18  |
| 25  |
| 30  |

---

## NULL 判断示例

```sql
SELECT phone
FROM contacts
WHERE phone IS NULL;
```
（6）

```sql
SELECT phone
FROM contacts
WHERE phone IS NOT NULL;
```
（7）

说明：
- `IS NULL` 用于查找字段值为 `NULL` 的记录
- `= NULL` 无效，比较不会成立
- `IS NOT NULL` 用于排除空值记录

**示例返回（IS NULL）：**

| phone   |
|---------|
| (null)  |
| (null)  |

**示例返回（IS NOT NULL）：**

| phone        |
|--------------|
| 13800138000  |
| 15555555555  |

---