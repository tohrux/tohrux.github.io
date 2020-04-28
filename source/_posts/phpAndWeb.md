---
title: php与Web的页面交互
date: 2019-12-06 09:26:13
tags:
- php
- web 
- 页面交互
- 前端
- 后端
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191207110525.png
---

# $_GET[] & $\_POST[]

究极全局变量 返回的是数组的形式

获取

```php
var_dump($_GET['username']);
```



# $_FILES[] 

返回的是数组形式的5个值

需要在html文件中如下设置:

```html
enctype="multipart/form-data"
```

# $_COOKIE[]

## 设置一个cookie

```php
setcookie('name','angelina',0,'/');//分别为 名称,内容,存在时间(为0的话意味着在页面关闭时就会删除该cookie),目录(不设置目录的话,只对当前目录有效)
```

## 判断cookie是否存在:

```php
isset(cookie['name']); //返回的是true or false
```

## 创建cookie数组

```php
setcookie("location[1]","beijing");
setcookie("location[2]","beijing");
setcookie("location[3]","beijing");

var_dump ($_COOKIE["location"]);
//输出数组形式
```

# $_SESSION[]

## 启动session

```php
session_start();
```

## 设置session

```php
$_session['username'] = "angelina";
$_session['age'] = 18;
```

### 销毁SESSION

```php
unset($_SESSION['username']);
或者使用session_destroy()函数来销毁全部
session_destroy();
```

👩即使使用了以上函数,但是由于php中的session是基于cookie的,所以session_id还存在于浏览器的cookie文件中需要调用cookie删除

```php
if (isset($_COOKIE[session_name()])){
    setcookie(session_name(),"",time()+1,"/");
}
```

