---
title: laravel控制器基础
date: 2019-11-22 10:05:01
tags:
- php
- laravel
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/laravel1.png
---

# 控制器文件的位置

控制器属于项目代码

位于**app/http/Controllers**

# 命名控制器文件

驼峰命名+Controller.php

# 控制器的结构代码

🚫不需要我们自己去写,可以通过artisan来生成

相应命令:

```cmd
php artisan make:controller TestController
```

创建资源控制器:(自动生成很多方法

```php
php artisan make:controller TestController --resource //简写 --r
```

分目录控制器(没有这个文件夹的话就会创建)

```cmd
php artisan make:controller Admin/TestController
```

创建成功的提示:

```cmd
Controller created successfully.
```



生成的结构代码:

```php
<?php

namespace App\Http\Controllers;//命名空间

use Illuminate\Http\Request;//命名空间三元素: 常量,方法,类

class TestController extends Controller
{
    //
}

```

# 控制器路由

#使用路由规则调用控制器下的方法,而不再走回调函数.

格式

```php
控制器类名@方法名
```

# 控制下的命名空间分组

```php
Route::group(['namespace'=>'Admin'],function(){
    Route:get('/shit/test1','TestController@test1')
})
```

# 接受用户输入

接受用户输入的类:illuminate\support\facades\input

**facades:介于一个类实例化与没有实例化之间的一个状态,是类的一个接口的实现,说白了就是静态方法.**

> 在laravel中如果需要使用facades,但是又不想写那么长:Use Illuminate\Support\Facades\Input 则可以在config/app.php中定义别名

```php
//自己添加的别名
        'Input' => Illuminate\Support\Facades\Input::class
```

👆👆👆👆👆👆👆👆👆👆👆👆👆👆👆

😤😤😤😤😤😤😤😤😤😤😤😤

上面真的是血的教训,我用的laravel是最新的6.5的,但是在5.2版本之后就开始用Request替代Input了

一开始疯狂检测自己的拼写,甚至重装laravel,花了大概一个半小时才解决了问题.

不过这个过程还是挺有意义的;

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request; //声明 这是自动生成的

class TextController extends Controller
{
    public function home(Request $request)//实例化对象
        
    {	
        //获取全部请求的数据
        dump($request->all());
		//只获取a,b字段的值
        dump($request->only(['a', 'b']));
		//获取除了a,b以外的值
        dump($request->except(['a', 'b']));
		//判断是否存在id的这个字段,exists完全等同于has
        dump($request->has('id'));

        dump($request->exists('id'));
		//获取id的值,如果请求字段为空的话就用 'xxx' 代替
        dump($request->input('id', 'xxx'));
        //"."可以用来分别获取每个数组元素
        dump($request->input('books.0'));
    }
}

```

