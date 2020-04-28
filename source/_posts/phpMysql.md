---
title: phpMysql -private
date: 2019-12-07 22:11:19
tags:
- php
- database
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191209180726.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191209180726.png
---

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191209180726.png)

# 访问数据库

1.连接数据库

```php
//使用 mysqli_connect()
```

2.选择服务器

```php
//使用 mysqli_select_db()来选择
```

3.执行数据库操作

```php
//增删改查四部曲

//
	insert into
//
    delete
//
    update
// 
    select
```

4.清除记录集,释放系统资源

```php
mysqli_free_result();
```

5.关闭MySQL服务器

```php
mysqli_close();
```

## 连接MySQL服务器

```php
$mysql = new mysqli($server,$username,$password,$dbname);
//$server 服务器地址 一般本地的为localhost
```

### mysqli 对象的内容

```php
mysqli Object
(
    [affected_rows] => 0
    [client_info] => mysqlnd 5.0.12-dev - 20150407 - $Id: 7cc7cc96e675f6d72e5cf0f267f48e167c2abb23 $
    [client_version] => 50012
    [connect_errno] => 0
    [connect_error] => 
    [errno] => 0
    [error] => 
    [error_list] => Array
        (
        )

    [field_count] => 0
    [host_info] => localhost via TCP/IP
    [info] => 
    [insert_id] => 0
    [server_info] => 5.5.5-10.4.8-MariaDB
    [server_version] => 100408
    [stat] => Uptime: 13265  Threads: 8  Questions: 163  Slow queries: 0  Opens: 29  Flush tables: 1  Open tables: 14  Queries per second avg: 0.012
    [sqlstate] => 00000
    [protocol_version] => 10
    [thread_id] => 82
    [warning_count] => 0
)
```



## 执行SQL语句

首先他们有两种风格 第二种是面向过程,略

### objdect oriented

```php
面向对象:
<?php
$serve = "localhost";
$user = "root";
$db = "jk";
$conn = new mysqli($serve, $user, "", $db);
//check connect 
if ($conn->connect_errno) {
    echo $conn->connect_error;
}
//insert into data
$sql = "insert into jkjk values(8,17,'peachx');";
$sql .= "insert into jkjk values(9,16,'peachxx');";
$sql .= "insert into jkjk values(10,16,'peachxs')";
$res = $conn->multi_query($sql);
var_dump($res);
//查询语句
$sql = "select * from jkjk";
$res = $conn->query($sql);
var_dump($res);//结果如下
```

👇

```php
mysqli_result Object
(
    [current_field] => 0
    [field_count] => 3
    [lengths] => 
    [num_rows] => 10
    [type] => 0
)
```

### 解析结果集

在使用完结果集后要记得使用结果集占用的内存

| 面向对象  $result->free_result(); |                      |
| --------------------------------- | -------------------- |
| free();close();**free_result()**  | mysqli_free_result() |

### 常用函数

| 面向对象($res = $conn->query($sql)) | description                                               |
| ----------------------------------- | --------------------------------------------------------- |
| fetch_row()                         | 以索引数组的方式返回一行数据                              |
| fetch_assoc()                       | 以关联数组的方式返回一行数据                              |
| fetch_array()                       | 以索引数组+关联数组的方式返回一行数据                     |
| fetch_object()                      | 以对象的方式返回一行数据                                  |
| num_rows                            | 返回数据的总行数                                          |
| data_seek()                         | 括号中必须给值,给0的话可以把fetch_*()中的数据偏移回初始行 |

### 开始查询

```php
while ($row = $res->fetch_assoc()) {
    print_r($row);
    // echo $row;
}

相当于👇
    
$res = $res->fetch_assoc();
print_r($res);
$res = $res->fetch_assoc();
print_r($res);
$res = $res->fetch_assoc();
print_r($res);  
......
```

 输出结果,这里只显示前三个

```php
Array
(
    [id] => 1
    [price] => 12
    [some] => apple
)
Array
(
    [id] => 2
    [price] => 12
    [some] => bnana
)
Array
(
    [id] => 3
    [price] => 14
    [some] => naizi
)
```

辛苦啦~





























