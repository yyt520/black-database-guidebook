---
nav:
  title: MySQL
  order: 2
group:
  title: 基础用法
  order: 3
title: 数据处理函数
order: 11
---

# 数据处理函数

## 文本处理函数

示例：将学生名字全部转为大写

```sql
SELECT name, UPPER(name) AS name_upper, age FROM students;

-- 输出
name      name_upper    age
------    ----------    --------
Irene     IRENE         19
Tony      TONY          19
Wolf      WOLF          18
Amy       AMY           16
Tom       TOME          15
```

常用的文本处理函数：

| 函数                                           | 说明                    |
| :--------------------------------------------- | :---------------------- |
| `LEFT()`（或使用子字符串函数）                 | 返回字符串左边的字符    |
| `LENGTH()`（也使用 `DATELENGTH()` 或 `LEN()`） | 返回字符串的长度        |
| `LOWER()`                                      | 将字符串转换为小写      |
| `LTRIM()`                                      | 去掉字符串左边的字符    |
| `RIGHT()`                                      | 返回字符串右边的字符    |
| `RTRIM()`                                      | 去掉字符串右边的空格    |
| `SOUNDEX()`                                    | 返回字符串的 SOUNDEX 值 |
| `UPPER()`                                      | 将字符串转换为大写      |

## 日期和时间处理函数

| 函数                                 | 说明                                              |
| :----------------------------------- | :------------------------------------------------ |
| `CURDATE()`                          | 返回当前日期                                      |
| `CURTIME()`                          | 返回当前时间                                      |
| `NOW()`                              | 返回当前的日期和时间                              |
| `UNIX_TIMESTAMP(date)`               | 返回日期 `date` 的 UNIX 时间戳                    |
| `FROM_UNIXTIME`                      | 返回 UNIX 时间戳的日期值                          |
| `WEEK(date)`                         | 返回日期 `date` 为一年中的第几周                  |
| `YEAR(date)`                         | 返回日期 `date` 的年份                            |
| `HOUR(time)`                         | 返回 `time` 的小时值                              |
| `MINUTE(time)`                       | 返回 `time` 的分钟值                              |
| `MONTHNAME(date)`                    | 返回 `date` 的月份名（英文）                      |
| `DATE_FORMAT(date, fmt)`             | 返回按字符串 `fmt` 格式化日期 `date` 值           |
| `DATE_ADD(date, INTERVAL expr type)` | 返回一个日期或时间值加上一个时间间隔的时间值      |
| `DATEDIFF(expr, expr2)`              | 返回起始时间 `expr` 和结束时间 `expr2` 之间的天数 |

MySQL 中的日期和时间格式：

| 格式符       | 格式说明                                                        |
| :----------- | :-------------------------------------------------------------- |
| `%S` 和 `%s` | 两位数字形式的秒（00, 01, ..., 59）                             |
| `%i`         | 两位数字形式的分                                                |
| `%H`         | 两位数字形式的小时，24 小时                                     |
| `%h` 和 `%I` | 两位数字形式的小时，12 小时                                     |
| `%k`         | 数字形式的小时，24 小时                                         |
| `%l`         | 数字形式的小时，12 小时                                         |
| `%T`         | 24 小时的时间形式（hh:mm:ss）                                   |
| `%r`         | 12 小时的时间形式（hh:mm:ssAM 或 hh:mm:ssPM）                   |
| `%p`         | AM 或 PM                                                        |
| `%W`         | 一周中每一天的名称（Sunday, Monday, ..., Saturday）             |
| `%a`         | 一周中每一天名称的缩写（Sun, Mon, ..., Sat）                    |
| `%d`         | 两位数字表示月中的天数（00, 01, ..., 31）                       |
| `%e`         | 数字形式表示月中的天数（1, 2, ..., 31）                         |
| `%D`         | 英文后缀表示月中的天数（1st, 2nd, 3rd）                         |
| `%w`         | 以数字形式表示周中的天数（0=Sunday, 1=Monday, ..., 6=Saturday） |
| `%j`         | 以 3 位数字表示年中的天数（001, 002, ..., 366）                 |
| `%U`         | 周（0, 1, ..., 52），其中 Sunday 为周中的第一天                 |
| `%u`         | 周（0, 1, ..., 52），其中 Monday 为周中的第一天                 |
| `%M`         | 月名（January, February, ..., December）                        |
| `%b`         | 缩写的月名（January, February, ..., December）                  |
| `%m`         | 两位数字表示的月份（01, 02, ..., 12）                           |
| `%c`         | 数字表示的月份（1, 2, ..., 12）                                 |
| `%Y`         | 4 位数字表示的年份                                              |
| `%y`         | 两位数字表示的年份                                              |
| `%%`         | 直接值 “%”                                                      |

### 日期和时间转换

示例：日期时间转换为时间戳

```sql
SELECT date_format("2022-01-19 19:45:20", "%Y%m%d%H%i%s");

-- 输出 20220119194520
+----------------------------------------------------+
| date_format("2022-01-19 19:45:20", "%Y%m%d%H%i%s") |
+----------------------------------------------------+
| 20220119194520                                     |
+----------------------------------------------------+
```

示例：日期转换字符串（必须带分隔符，常用中划线 `-` 作为日期分隔符）

```sql
SELECT date_format("2022-01-19 19:45:20", "%Y-%m-%d");
-- 输出 2022-01-19
+------------------------------------------------+
| date_format("2022-01-19 19:45:20", "%Y-%m-%d") |
+------------------------------------------------+
| 2022-01-19                                     |
+------------------------------------------------+
```

示例：时间转换字符串（必须带分隔符，常用冒号 `:` 作为时间分隔符）

```sql
SELECT date_format('2022-01-19 19:45:20', '%H:%i:%s');
-- 输出 19
+------------------------------------------------+
| date_format('2022-01-19 19:45:20', '%H:%i:%s') |
+------------------------------------------------+
| 19:45:20                                       |
+------------------------------------------------+
```

### 日期时间运算

**向后偏移时间**

示例：获取今天之后 `n` 天对应的日期，就是相当于在今天日期的基础上加 `n` 天

```sql
SELECT
  "2022-01-01" AS col1,
  date_add("2022-01-01", interval 7 year) AS col2,
  date_add("2022-01-01", interval 7 month) AS col3,
  date_add("2022-01-01", interval 7 day) AS col4;

-- 输出
+------------+------------+------------+------------+
| col1       | col2       | col3       | col4       |
+------------+------------+------------+------------+
| 2022-01-01 | 2029-01-01 | 2022-08-01 | 2022-01-08 |
+------------+------------+------------+------------+

SELECT
    "2022-01-01 01:01:01" AS col1,
    date_add("2022-01-01 01:01:01",interval 7 hour) AS col2,
    date_add("2022-01-01 01:01:01",interval 7 minute) AS col3,
    date_add("2022-01-01 01:01:01",interval 7 second) AS col4;
```

**向前偏移时间**

示例：

```sql
SELECT
    "2022-01-01" AS col1
    date_sub("2022-01-01",interval 7 year) AS col2,
    date_sub("2022-01-01",interval 7 month) AS col3,
    date_sub("2022-01-01",interval 7 day) AS col4;
```

**两日期之差**

示例：使用 `dateddiff` 返回两日期之间相差的天数

```sql
SELECT datediff("2022-01-07","2022-01-01")

-- 输出
6
```

## 数值处理函数

常用数值处理函数

| 函数     | 说明               |
| :------- | :----------------- |
| `ABS()`  | 返回一个数的绝对值 |
| `COS()`  | 返回一个角度的余弦 |
| `EXP()`  | 返回一个数的指数值 |
| `PI()`   | 返回圆周率         |
| `SIN()`  | 返回一个角度的正弦 |
| `SQRT()` | 返回一个数的平方根 |
| `TAN()`  | 返回一个角度的正切 |
