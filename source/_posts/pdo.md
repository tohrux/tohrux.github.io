---
title: pdo
date: 2019-12-11 20:00:06
tags:
- pdo
- php
- database
- mysql
- 数据库
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191211200234.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191211200234.png
---

PDO,php data object *php数据对象*

# 连接服务器

比php连接mysql多了一个参数,数据库类型

**$dbms** *Database Management System*

**$dsn** *Data Source Name*

```php
<?php
echo "<pre>";
$dbms = 'mysql';
$host = 'localhost';
$dbName = 'jk';
$user = 'root';
$pass = '';
$dsn = "$dbms:host=$host;dbname=$dbName";
// echo $dsn;

try{
    //去try,去执行,去创建,这个pdo对象
    $pdo = new PDO($dsn,$user,$pass);
    echo "success";
} catch(PDOException $e){
   //如果try中内容有错误,则会在catch中捕获异常;即对象没有创建成功,则会执行catch里面的内容,捕获异常的时候要使用PDO自己的异常处理类 "PDOException $e"
    
   die($e->getMessage());  //因为没有必要往下进行了,所以直接die打印出$e->getMessage()
}
```

# 执行sql语句

## exec() 需要结果集的sql语句

insert into ,delete ,update

```php
$sql = "insert into jkjk2 (name) values ('popo')";
$ret = $pdo->exec($sql);
print_r($ret); //受影响的行
```



## query() 不需要结果集的sql语句

```php
$sql = "select * from jkjk2";
$ret = $pdo->query($sql);
print_r($ret);
```

👇

```php
PDOStatement Object//预处理对象
(
    [queryString] => select * from jkjk2
)
```

再使用foreach循环出 PDOStatement Object中的数据

```php
foreach($ret as $row){
    var_dump($row);
}
```

👇

```php
array(4) {
  ["id"]=>
  string(1) "1"
  [0]=>
  string(1) "1"
  ["name"]=>
  string(4) "popo"
  [1]=>
  string(4) "popo"
}
array(4) {
  ["id"]=>
  string(1) "2"
  [0]=>
  string(1) "2"
  ["name"]=>
  string(3) "din"
  [1]=>
  string(3) "din"
}
array(4) {
  ["id"]=>
  string(2) "17"
  [0]=>
  string(2) "17"
  ["name"]=>
  string(5) "jiill"
  [1]=>
  string(5) "jiill"
}
```

# 预处理语句

PDO使用PDOStatemendeadaot来实现预处理语句,这个类的实例可以用query()方法得到,也可以用prepare(),区别是query()只能得到一条sql命令的数据集的结果,而prepare()得到的实例可以重复执行sql语句

```php
    //prepare() 预处理语句
//数据占位符
    $pre = $pdo->prepare("insert into jkjk2 (id,name)values(?,?)");
    $id = 3;
    $name = "id3";
    $pre -> bindParam(1,$id);
    $pre -> bindParam(2,$name);
    $pre -> execute(); 
//直接用数组写
    $pre -> execute(array(
        4,"id4"
    ));
//命名参数
    $pre = $pdo -> prepare("insert into jkjk2 (id,name) values (:id,:name)");
    $id = 7;
    $name = "id7";
    $pre->bindValue(":id",$id);
    $pre->bindValue(":name",$name);
    $pre->execute();
//关联数组
    $pre -> execute(array(
        ":id" => 6,
        ":name" => "id6"
    ));

```



# 解析结果集

## $result -> fetch(PDO::FETCH())

```php
  var_dump($result -> fetch());//仅仅输出一条
  var_dump($result -> fetchAll(PDO::FETCH_NUM));//剩下的所有的结果以索引数组的方式输出
//$result -> fetchAll(PDO::FETCH_OBJ/ASSOC/NUM)
```

## $result -> fetchColumn(*)

*为可选的数字 默认为0,从0开始,表示第一列

整个函数返回的是下一行的结果的第*列

# SQL注入

利用sql的查询语句恶意获取数据库信息



# 完结撒花~!

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191213091052.png)







