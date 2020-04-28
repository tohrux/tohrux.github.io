---
title: mysql
date: 2019-12-09 18:45:51
tags:
- mysql
- database
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191209190454.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191209190454.png
---

 ![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191209190454.png)

### 创建数据库

```mysql
create database 数据库名;
```

### 选择数据库

```mysql
use 数据库名;
```

### 删除数据库

```mysql
drop database 数据库名;
```

# 创建数据表

```mysql
CREATE TABLE 数据表名 (字段名 字段类型);

CREATE TABLE `tbl`(
   `id` INT UNSIGNED AUTO_INCREMENT,
   `title` VARCHAR(100) NOT NULL,
   `author` VARCHAR(40) NOT NULL,
   `date` DATE,
   PRIMARY KEY ( `id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;//引擎和格式
```

#### comment 关键字

后面跟上字符串 表示注释

#### default关键字

后面跟不给值时的默认选项

#### unique

可以为空甚至一直为空

#### primary key

primary key = unique + not null

### insert into

```mysql
insert into tb1 (id,title,date) values (1,'one','2010-1-1');
or
insert into tb1 values(2,'two','2019-9-9');
```

### delete

```mysql
delete from tb1 where id=1;
```

### update

```mysql
update tb1 set title = "love" where id=1;
```

### select 

```mysql
select * from tb1;
```

# 查询

不等于: `<>` `!=`

## 关键字

### between&and

```mysql
select * from tb1 where id between 1 and 3;
```

👩:包括1和3

```mysql
select * from tb1 where id<3 and id>1;
```

### in

!@!!@!@!@!@!!@!@!@!@!@

```mysql
select * from tb1 where id in(1,2,3);
```

### union & unionall

可以从不同的表中返回查询结果并结合在一起,

区别是union会在unionall的基础上进行一次 `distinct` 查询

### DISTINCT

 *adj. 明显的；独特的；清楚的；有区别的*

`select DISTINCT 字段 from 表名`

排除重复的查询结果



### group by

默认时ascend;

在 group by 后面可以跟上多个字段或者加上order by也行

## 模糊查询

### like关键字

`select 字段 from 表名 where 字段 like 值`

` %u% `

 `%` 用来匹配0个或多个字符,任意类型,任意长度,没有限制

`_u_`

`_`匹配任意单个字符

## 排序查询

### order by

默认ascend

```mysql
select * from tb1 order by id desc/asc;
```

👩:descend / ascend

## 限制查询

`select 字段 limit 起始偏移量,行数`

## 聚合

`count(*)` `sum(字段名)` `max(字段名)`  `min(字段名)` 

 `with rollup`表示对聚合分类后的对象再进行汇总

`having`分类聚合后的限制条件要用having而不是`where`;

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191210150306.png)

👩:可以直接进行计算

```mysql
mysqli
```



## 连接

#### inner join 

内连接,获取两个表中字段匹配关系的记录 (两个表中的重叠部分)

### left join

左连接,获取表中的所有记录,即使右边没有对应的匹配记录

### right join

同上

# 事务

回滚 rollback

提交 commit

四大特性: 原子性, 一致性 ,隔离性, 持久性



# 子段操作

增

```mysql
alter table 数据表名 add 新增字段 字段类型;
```

删

```mysql
alter table 数据表名 drop 字段名;
```

修改字段类型:

```mysql
alter table modify 字段名 数据类型;
```

修改表名:

```mysql
alter table 数据表名 rename 新表名
```

修改字段名

```mysql
alter table change 字段名 新字段名 新数据类型
```





# 索引

### 创建索引

1,创建普通索引,在创建表的时候创建索引

```mysql
create table index1(
	id INT,
    name VARCHAR(32),
    INDEX(id)
)

```

or

```mysqli
 mysql> CREATE TABLE `jkjk` (  

    ->   `id` smallint(8) unsigned NOT NULL,  
    ->   `catid` smallint(5) unsigned NOT NULL DEFAULT '0',  

    ->   `title` varchar(80) NOT NULL DEFAULT '',  
     ->   `content` text NOT NULL,  

   ->   PRIMARY KEY (`id`),  

    ->   UNIQUE KEY `catename` (`catid`)  

    -> ) ;  
```



UNIQUE /FULLTEXT

```mysql
create table index1(
	id INT,
    name VARCHAR(32),
    UNIQUE INDEX index_1(id ASC)
)
```

2,用alter table创建索引

```mysql
alter TABLE 表名 ADD primary key (字段名); 
```

3,用create index 创建索引

```mysql
create 索引类型 INDEX 索引名 ON 表名(字段名);
```

eg:

```mysql
create UNIQUE INDEX index_1 ON tb1(id);
mysql> CREATE UNIQUE INDEX catename ON wb_blog(catid); 
```

### 删除索引

```mysql
DROP INDEX index_1 on tb1;
```

### 查看索引

```mysql
SHOW INDEX from tb1;
```

