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