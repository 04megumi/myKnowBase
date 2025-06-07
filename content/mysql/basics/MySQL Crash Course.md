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