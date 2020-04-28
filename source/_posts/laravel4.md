---
title: laravel中关于数据库的操作
date: 2019-11-22 20:28:14
tags:
- php
- laravel
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/laravel1.png
---

# 所有项目都由这六个部分组成

1. 增删改查
2. 循环
3. 判断

# DB类操作数据库

按照MVC架构,对数据的操作都应该放在Model中完成.但如果不使用Model,也可以在laravel框架提供的DB类数据库操作数据.laravel中DB类的基本用法:**DB::table('tableName')**

在对数据库进行操作使用的是**navicat**

1. new 一个新的数据库 **qz04**

2. 在 **qz04**下 new 一个新的table **member**

3. 新建查询,代码如下:

```mysql
create table member(
    id int primary key auto_increment,
    name varchar(32) not null,
    age tinyint unsigned not null,
    email varchar(32) not null
)engine myisam charset utf8;
```

4. 在laravel中对 **.env**文件进行修改,链接到数据库

   ```txt
   DB_CONNECTION=mysql
   DB_HOST=localhost
   DB_PORT=3306
   DB_DATABASE=qz04
   DB_USERNAME=root
   DB_PASSWORD=
   ```

5. 在TextController控制器中引入DB门面

   ```php
   use DB;//因为已经在app.php文件中定义,所以可以直接use
   ```

6. 在web.php注册路由

   ```php
   //增删改查
   Route::group(['prefix' => 'home/index'], function () {
       Route::get('/add', "TextController@add");
       Route::get('/del', "TextController@del");
       Route::get('/update', "TextController@update");
       Route::get('/select', "TextController@select");
   });
   ```

   

## 增加信息(insert)

▶**insert(数组)可以同时添加一条或多条,返回的是布尔类型**

```php
DB::table('无前缀表名') -> insert(); //链式操作;
```



向member表同时添加多条数据:

```php
    public function add()
    {
        //定义相关联的表名
        $db = DB::table('member');
        //使用insert增加数据
        $result = $db->insert([
            [
                'name' => '安洁莉娜',
                'age'  => '17',
                'email' => 'angelina@gmail.com'
            ],
            [
                'name' => '艾雅法拉',
                'age'  => '17',
                'email' => 'eyjafjalla@gmail.com'
            ],
            [
                'name' => '陈',
                'age'  => '17',
                'email' => 'chen@gmail.com'
            ]
        ]);
        dd($result);//返回为true
    }
```

extra🤹‍♀️: 也可以使用以下方法进行 **insert** 的操作:

```php
$db = DB::table('member');
$result = $db-> insertGetId([
    'name' => '马冬梅',
     ...
])
dd($result);//返回id的值;
```

## 修改数据(update)

▶修改数据可以使用where('字段名','符号','值')  -> update([]); 如下:

```php
  public function update()
    {
        //定义需要操作的数据表
        $db = DB::table('member');
        //修改id为1的用户的name
        $result = $db->where('id', '=', '1')->update([
            'name' => '安洁莉娜是jk'
        ]);
        dd($result); //👩返回1 表示为收到影响的行数
    }
```

## 查询数据

```php
▶DB:table('member')->get(); //相当于 select * from member;
```

```php
    public function select()
    {
        $db = DB::table('member');
        $result = $db->get();
        //尝试循环遍历数组
        foreach ($result as $key => $value) {
            dump($value);
        }
        //获取指定范围的数据
        $kk = $db->get()->where('id', '<', '3')->where('id', '>', '1');
        //获取where('id', '<', '3')中的第一行数据
        $kk1 = $db->get()->where('id', '<', '3')->first();
        dump($kk);
        dump($kk1);
    }
```

按照指定字段进行特定规则的排序

```php
$kk2 = DB::table('member')->orderBy('age', 'desc')->get();
```

分页操作

```php
$kk3 = DB::table('member')->limit(2)->offset(2)->get();
//limit(x) x:最多显示的行数 offset(y) y:从第y行开始取
```

## 删除数据(delete)

删除中有两种方式,第一种是物理删除(本质是删除),**逻辑删除(本质是修改);**

数据删除可以通过delete函数和truncate函数实现,

```php
Delete 表示删除记录;
Truncate 表示清空整个数据表;
```

```php
$db = DB::table('member');
$result = $db->where('id', '=', '1')->delete();//返回的是受影响的行数;
```

# 书上的增删改查的方法



