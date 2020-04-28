---
title: laravel的继承与包含(extend&include 
date: 2019-11-25 18:50:08
tags:
- php
- css
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/laravel1.png
---

# @include

可以用来引进别的页面

```php
@include('文件名')
```



# @extends

```php
父级页面 语法:@yield('名字') 
```

```php
子级页面:@extends('view下的路径')
@section('名字')
内容
@endsection
```

**实例**:

父级页面:

```php
<h1>我是头部</h1>
{{-- 可变区 --}}
@yield('myBody')
{{-- 可变区 --}}
<h1>我是尾部</h1>
```

子级页面:

```php
@extends('test/test2')
@section('myBody')
<h1>
    Lorem ipsum dolor sit amet consectetur a
    dipisicing elit. Ea quibusdam quas nobis minima, aspernatur laborum nihil, natus omnis quia solu
    ta beatae recusandae deleniti neque
    ? Voluptatibus, nulla mollitia. Possimus, laborum adipisci?
</h1>
@endsection
```

结果:

```php
我是头部
Lorem ipsum dolor sit amet consectetur a dipisicing elit. Ea quibusdam quas nobis minima, aspernatur laborum nihil, natus omnis quia solu ta beatae recusandae deleniti neque ? Voluptatibus, nulla mollitia. Possimus, laborum adipisci?
我是尾部
```
