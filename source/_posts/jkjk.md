---
title: lavavel视图
date: 2019-11-24 13:32:50
tags: 
- laravel
- php
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/laravel1.png
---

# 视图文件的命名和渲染

1. 文件名习惯小写
2. 后缀为 **blade.php** 
3. 不使用 **balde.php**结尾的话就不能使用laravel提供的标签{{$title}}语法显示数据,只能使用原生语法显示数据

# 实例

在开发中可以使用compact(php内置函数)来进行数组的打包

### TextController:

```php
    public function test3()
    {
        //现在时间
        $date = date('Y-m-d H:i:s', time());
        //获取今天的星期
        $day = 'sunday';
        //show 视图
        //return view('home/index/test3', ['date' => $date, 'day' => $day]);
        👆
      效果一样   
         👇
        return view('home/index/test3', compact('date', 'day'));
    }
```

### web.php:

```php
Route::get('/home/index/test3', "TextController@test3");
```

### text3.blade.php:

```php
当前访问的是home/index/test3.blade.php文件<br/>
现在是: {{$date}},今天是星期{{$day}}
```

### 输出:

```html
当前访问的是home/index/test3.blade.php文件
现在是: 2019-11-23 01:47:37,今天是星期sunday
```

### 之前输出当前时间:

```php
时间戳 {{date('Y-m-d H:i:s',$time)}}
```

### 一年后的时间:

```PHP
{{date('Y-m-d H:i:s',strtotime('+1 year'))}};
```

# 循环分支语法标签

下面是一个案例

**Controller**中:

```php
use DB;

class TestController extends Controller
{
    //start
    public function test1()
    {
        $db = DB::table('member')->get();
        // dd($db);
        return view('test.test1', compact('db'));
    }
}

```



**blade**中:

```php
id&emsp;&emsp;name&emsp;&emsp;email&emsp;<br>
@foreach ($db as $key => $value)
{{-- 如果不要key的话可以直接省略 ($db as $value) --}}
    {{$value -> id}}&emsp;&emsp;
    {{$value -> name}}&emsp;&emsp;
    {{$value -> email}}
    <br>
@endforeach

```

**输出结果:**

```html
id  name  email 
1   阿龙   al@gmail
2   阿B   ab@gmail
```

🙋‍特别注意

get查询道德结果集中的每一条都是一个对象,因此在循环具体字段的时候需要注意使用对象调用属性的方式才可以获取其数据

# 判断语句

```php
if在模板引擎的写法
@if (Expression1)
statement1
@elseif(Expression2)
statement2
...
@else
statement3
@endif
```

