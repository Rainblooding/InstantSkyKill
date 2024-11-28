---
abbrlink: ''
categories:
- - mysql
date: '2024-11-28T14:12:08.953824+08:00'
tags:
- mysql
title: mysql中数字相加的问题
updated: '2024-11-28T14:18:22.962+08:00'
---
今天天在写sql的时候遇到了一些问题，记录一下

```sql
select 1
select 1 + null
```

在第二种情况下得到的结果会是`null`，这与业务不相符，所有我们要改成其他格式来避免这个问题

```sql
select 1 + ifnull(subSql,0)
```

试用`ifnull`函数当子语句为`null`时会转换为`0`，避免了上面的情况
