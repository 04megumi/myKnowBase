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

# MySQL 基础使用：数据过滤

日期：2025-06-07  
作者：SeraphimWei  
参考书籍：MySQL Crash Course（第 7 章）

---

## 组合 WHERE 条件（AND）

```sql
SELECT c1, c2, c3
FROM table_name
WHERE c1 = 't1' AND c2 <= 100;
```
（1）

说明：必须同时满足所有条件（逻辑与）

---

## 使用 OR（或）

```sql
SELECT name, age
FROM users
WHERE age < 18 OR age > 60;
```
（2）

说明：只要满足任一条件即可（逻辑或）

---

## 计算次序：AND 优先于 OR

```sql
SELECT name
FROM users
WHERE gender = 'female' AND age > 18 OR score >= 90;
```
（3）

等价于：

```sql
-- 实际执行顺序：
SELECT name
FROM users
WHERE (gender = 'female' AND age > 18) OR score >= 90;
```

说明：AND 优先于 OR，建议用括号明确表达逻辑

---

## 使用括号明确优先级

```sql
SELECT name
FROM users
WHERE gender = 'male' AND (age < 18 OR age > 60);
```
（4）

说明：仅当性别为男，且年龄不在 18 到 60 之间时才匹配

---

## 使用 IN 判断多个值

```sql
SELECT name
FROM students
WHERE class IN ('A1', 'A2', 'A3');
```
（5）

说明：等价于 `class = 'A1' OR class = 'A2' OR class = 'A3'`，常用于多值匹配

---

## 高级用法：IN + 子查询

```sql
SELECT name
FROM users
WHERE dept_id IN (
  SELECT id FROM departments WHERE location = 'Beijing'
);
```
（6）

说明：从子查询结果中取值匹配，常用于多表过滤

---

## 使用 NOT 排除条件

```sql
SELECT name
FROM employees
WHERE NOT (department = 'HR');
```
（7）

或与 IN 配合：

```sql
SELECT name
FROM students
WHERE class NOT IN ('A1', 'A2');
```
（8）

---

## WHERE 逻辑操作符对比表

| 操作符 | 描述               | 示例                                      |
|--------|--------------------|-------------------------------------------|
| AND    | 与（同时满足）     | `WHERE age > 18 AND gender = 'male'`      |
| OR     | 或（任一满足）     | `WHERE age < 18 OR age > 60`              |
| ()     | 括号控制优先级     | `WHERE (a AND b) OR c`                    |
| IN     | 属于某集合         | `WHERE country IN ('US', 'UK', 'CN')`     |
| NOT    | 非，取反           | `WHERE NOT status = 'done'`               |
| NOT IN | 不属于某集合       | `WHERE dept NOT IN ('HR', 'Sales')`       |

---

## 示例数据表：users

| id | name  | age | gender | dept     |
|----|-------|-----|--------|----------|
| 1  | Alice | 25  | female | HR       |
| 2  | Bob   | 17  | male   | Dev      |
| 3  | Carol | 65  | female | Finance  |
| 4  | Dave  | 30  | male   | Sales    |
| 5  | Eve   | 15  | female | HR       |

**示例：**

```sql
SELECT name
FROM users
WHERE gender = 'female' AND (age < 18 OR age > 60);
```

**返回：**

| name  |
|-------|
| Carol |
| Eve   |

---

# MySQL 基础使用：用通配符进行过滤

日期：2025-06-07  
作者：SeraphimWei  
参考书籍：MySQL Crash Course（第 8 章）

---

## 通配符过滤简介（LIKE）

`LIKE` 表示使用通配符进行模式匹配，而不是使用 `=` 进行精确匹配。

常见通配符：

| 通配符 | 含义                         |
|--------|------------------------------|
| `%`    | 任意长度的任意字符（含0个） |
| `_`    | 任意单个字符                 |

---

## 使用 `%` 匹配以某字符开头

```sql
SELECT name
FROM users
WHERE name LIKE 'Jet%';
```
（1）

说明：匹配所有以 `Jet` 开头的字符串，如 `Jet`, `Jetson`, `Jet Lee`。

---

## 使用 `%` 匹配包含某关键词

```sql
SELECT name
FROM users
WHERE name LIKE '%xxx%';
```
（2）

说明：匹配任意包含 `xxx` 的字符串（前后都有可能出现其他字符）

---

## 使用 `%` 匹配以某字符开头和以某字符结尾

```sql
SELECT name
FROM users
WHERE name LIKE 's%e';
```
（3）

说明：匹配以 `s` 开头、以 `e` 结尾的任意字符串，如 `Steve`、`spare`。

---

## `%` 可匹配 0 个字符

```sql
SELECT name
FROM users
WHERE name LIKE 'Ann%';
```

匹配 `Ann`、`Annabelle`，也包括只包含 `Ann` 的项。

---

## 注意：尾部空格影响匹配

示例数据：

| name      |
|-----------|
| 'Bob'     |
| 'Bob '    |

查询：

```sql
SELECT name
FROM users
WHERE name LIKE 'Bob';
```

说明：只会匹配 `'Bob'`，不会匹配 `'Bob '`（含空格）

---

## 注意：LIKE 不会匹配 NULL

```sql
SELECT name
FROM users
WHERE name LIKE '%a%';
```

说明：`name IS NULL` 的记录不会匹配，即使有 `%`，NULL 也不参与字符串匹配。

---

## 使用 `_` 通配符：匹配单个任意字符

```sql
SELECT code
FROM products
WHERE code LIKE '_A%';
```
（4）

说明：匹配第二位是 `A` 的字符串，如 `1A45`、`BA78`，但不匹配 `AA123`。

---

## 下划线 `_` 示例

| code   |
|--------|
| A123   |
| AB23   |
| BA23   |
| 1A45   |
| A_23   |

查询示例：

```sql
SELECT code
FROM products
WHERE code LIKE '__23';
```

结果匹配：`AB23`, `BA23`, `A_23`（前两位任意字符，后两位固定是 2 和 3）

---

## 小结：通配符使用建议

| 特性               | 建议/说明                             |
|--------------------|----------------------------------------|
| `%` 匹配任意字符   | 尾部匹配较快，前置 `%` 效率差          |
| `_` 匹配一个字符   | 用于匹配特定位数                      |
| 匹配 NULL 无效     | `LIKE` 不会匹配 NULL 值               |
| 尾部空格敏感       | `LIKE 'Bob'` 不等于 `LIKE 'Bob '`     |
| 不建议滥用         | `%xxx%` 查询无法使用索引，性能较差     |

---

## 示例表：users

| id | name      |
|----|-----------|
| 1  | Jet       |
| 2  | Jetson    |
| 3  | Steve     |
| 4  | sarge     |
| 5  | Jet Lee   |
| 6  | Bob       |
| 7  | Bob       |
| 8  | Bob       |
| 9  | NULL      |

```sql
SELECT name
FROM users
WHERE name LIKE 'Jet%';
```

返回结果：

| name    |
|---------|
| Jet     |
| Jetson  |
| Jet Lee |

---