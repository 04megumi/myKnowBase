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
USE <database_name>;
```
（3）

---

## 查看数据库

```sql
SHOW DATABASES;
```
（4）

---

## 查看数据表

```sql
SHOW TABLES;
```
（5）

---

## 查看表结构

```sql
SHOW COLUMNS FROM <table_name>;
-- 或
DESCRIBE <table_name>;
```
（6）

---

## 查看服务器状态

```sql
SHOW STATUS;
```
（7）

---

## 查看当前用户权限

```sql
SHOW GRANTS;
```
（8）

---

## 查看错误与警告

```sql
SHOW ERRORS;
SHOW WARNINGS;
```

# MySQL 基础使用：检索数据

日期：2025-06-07  
作者：SeraphimWei  
参考书籍：MySQL Crash Course（第 4 章）

---

## 基本 SELECT 查询

```sql
SELECT column_name
FROM table_name;
```
（1）

---

## 查询多个列

```sql
SELECT column1, column2, ...
FROM table_name;
```
（2）

---

## 查询所有列

```sql
SELECT *
FROM table_name;
```
（3）

---

## 去重查询

```sql
SELECT DISTINCT column_name
FROM table_name;
```
（4）

---

## 限制返回行数

```sql
SELECT column_name
FROM table_name
LIMIT N;
```
（5）

说明：
- `LIMIT N`：返回前 N 行数据

---

## 分页查询

```sql
SELECT column_name
FROM table_name
LIMIT offset, count;
```
（6）

说明：
- `offset` 表示起始行索引（从 0 开始）
- `count` 表示返回的行数

示例：

```sql
SELECT name
FROM students
LIMIT 10, 5;
-- 从第 11 行开始返回 5 行
```

---
