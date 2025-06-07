# MySQL Basics

This section covers the foundational concepts and commands of MySQL, including:

- SQL syntax and query structure
- Database creation and management
- Basic CRUD operations
- Indexes and constraints

本章节记录 MySQL 的基础知识，包括：

- SQL 语法与查询结构
- 数据库的创建与管理
- 基础增删改查操作
- 索引与约束基础

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
