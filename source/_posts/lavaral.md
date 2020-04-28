---
title: laravel路由规则的使用
date: 2019-11-21 08:34:08
tags:
- php
- laravel
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/laravel1.png
---

# 4种常用的路由方法

post/get/any/match

```php
//get 语法
//例如访问/hey的时候可以这样写
Route::get ('/hey', function() {
    return "hello";
});


//post
//post方法可以用postman来获取值
//👩post请求需要在VerifycsrfToken中修改把不想要csrf请求的路由写在这里:
	protected $except = [
        //把不想csrf验证得路由写在这里
        '/hello'
    ];
Route::post ('/hello', function() {
    return "hello from post";
});



//any
//任意类型
Route::any('/test2', function () {
    echo '当前是用any访问';
});
//match
Route::match(['get', 'post'], '/test3', function () {
    echo '当前是用match访问';
});
```

# 路由参数

路由参数其实就是给路由传递参数

参数分为**必选参数**和**可选参数**

```php
//必选参数 给定默认值
Route::any('users/{id}', function ($id='') {
    echo '当前用户的id是'.$id;
});
👆这样写会报错,不能预先给定值,必须要用户输入数字才可以
    eg:example.com/users/123  //输出 当前用户的id是123
//可选参数 给定默认值
Route::any('users2/{id?}', function ($id='') {
    echo '当前用户的id是'.$id;
});
👆可预先给定值
//通过?形式传递get参数
Route::any('/user3', function () {
    echo '当前用户的id是'.$_GET['id'];
});
//限制路由参数 例如:必须是数字 必须有参数
Route::get('hello2/{id}', function ($id) {
    echo "now is".$id;
}) -> where('id','[0-9]+');
```

# MVC

使代码不累赘

c --处理用户交互逻辑,如果需要交互就会跳到mdel处理数据

else -> 直接跳转到view

model --用于处理数据的增删改查

# 路由别名

```php
//路由别名
//🙅不可以直接输入到地址栏,但是可以作为简写被别的方法调用
Route::any('/user4/afadfaf/asdfasfasdf/asdfasd', function () {
    echo 'IamUser4';
}) -> name('user4');
Route::get('/na', function () {
    return redirect()->route('user4');
});

Route::group(['prefix' => 'admin'], function () {
    Route::get('/test1', function () {
        return 'IamTest1';
    });
    Route::get('/test2', function () {
        echo "IamTest2";
    });
});
```



# 查看系统当前路由别名

在laravel根目录下cmd -> php artisan可以查看所有命令, 找到route:list(这代表了路由列表,然后再cmd -> php artisan route:list  🆗

# 路由群组:

如果路由层级过多,每次要重新定义路由会很麻烦,我们可以将前缀一样的路由放在路由群组里

```php
Route::group(['prefix' => 'admin'], function () {
    Route::get('/test1', function () {
        return 'IamTest1';
        //匹配 "/admin/test1" URl
    });
    Route::get('/test2', function () {
        echo "IamTest2";
        //匹配 "/admin/test2" URl
    });
    Route::group(['prefix' => '/test1'], function () {
        Route::get('/login', function () {
            return '我是二级路由test1下面的三级路由login';
        });
    });
});
👆以上代码中admin被称为一级路由,test1/test2被称为2级路由,以此类推
```

# 限制路由参数 

```php
//限制路由参数 例如:必须是数字 必须有参数
Route::get('hello2/{id}', function ($id) {
    echo "now is".$id;
}) -> where('id','[0-9]+');
```

