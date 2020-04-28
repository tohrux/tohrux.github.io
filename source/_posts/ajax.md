---
title: AJAX JSON对象 XML -private
date: 2019-12-03 08:49:39
tags:
- ajax
- javascript
- jQuery
- 前端
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191203123124.png
---

*笔记来源于书*

### 原生ajax写法

```js
      	var xhr = new XMLHttpRequest();
        //
        xhr.open("post", "test.php");
        //
        xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
        //
        xhr.send("a=1&b=10");
        //
        xhr.onreadystatechange = function () {
            if (xhr.status == 200 && xhr.readyState == 4) {
                var result = xhr.responseText;
                alert(result);
            }
        }
```

👩: 在上面的代码中:

​	1.`XMLHttpRequest()`是ajax的一个内置对象,能知道传值的地址,传地数据和传递数据的方式

​	2.`open()`,初始化`XMLHttpRequest`对象,指定http请求的方法和要使用的服务器的URL;

​			格式:`open(method: string, url: string): `

​	3.`send()`,发送该请求,指定发送的数据,如果http请求是`get`,可以不指定参数,或者用null..

​	4. `status==200`:成功处理了请求，一般情况下都是返回此状态码

 	5. `readyState==4` 请求完成加载
 	6. `onreadystatechange`:XMLHttpRequest调用的时间处理器,他会检测readystate和http的状态,即上面的4和5.

### jQuery中的ajax的写法

```js
 $.ajax({
            url: '',
            type: 'post|get',
            data: '数据',
            dataType: 'text|json|xml|script',
            success: function (re) {
                //服务器回传的数据处理
            }
        })
```

### JSON对象

可以理解为有格式的字符串,以键值的形式存放;他的作用是存放数据

有两种格式:

```
{name:'angelina',age:19};
```

```js
[{name:'angelina',age:19},{name:'angelina',age:19},{name:'angelina',age:19}]
```

两种格式的结合:

```js
{list:[{name:'angelina',age:17},{name:'eyjfjalla',age:18}]}
```

### 对象解析为JSON对象

`JSON.stringify(Object)`

### 字符串解析为JSON对象

JSON.parse({...,..,...})

### JSON传值

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery-3.4.1.js"></script>
    <script type="text/JavaScript">
        var aStudent = {
            name: 'angelina',
            age: 18
        };
        var students = [{
            name: 'a',
            age: 12
        }, {
            name: 'b',
            age: 13
        }];

        $(function () {
            var n;
            var a;
            for (var k in students) {
                n = students[k].name;
                a = students[k].age;
                $("#s").append("<tr><td>"+n+"</td><td>"+a+"</td></tr>");
            }
        })
    </script>
</head>

<body>
    <h1>JSON:</h1>
    aStudent的名称:
    <script type="text/JavaScript">document.write(aStudent.name)</script>
    <br />
    students的第一个名称:
    <script>
        document.write(students[0].name)
    </script>
    <table id="s" border="1">
        <tr>
            <th>name</th>
            <th>age</th>
        </tr>

    </table>
</body>

</html>
```

### XML的基本格式

```xml
<?xml version="1.0" encoding="utf-8" ?>
<list>
    <province id="1" name="河北">
        <city id="11" name="石家庄"></city>
        <city id="12" name="承德"></city>
    </province>
</list>
```

### load()

语法:

```js
$(selector).load(url,data,callback)
```

url:文件地址

data: 规定与请求共同发送的查询字符串键值对的集合,是可选的

fallback: 回调函数,可选的

👇

fallback里面可以有三个值:

```js
$('#who').load("book.html", function (responseText, statusText,xhr){}
```

responseText为返回的调用成功后的结果内容

statusText为调用的状态,成功的话会 返回 "success"

xhr 为整个XMLHtmlRequest对象

👩:可以通过console log 来check it out

```js
$(function () {
            $('.button2').click(function () {
                $('#who').load("book.html", function (responseText, statusText, xhr) {
                    console.log(xhr.status);
                    console.log(xhr.responseText);
                    console.log(xhr.statusText);
                    console.log(responseText);
                    console.log(statusText);
                });
            })
        })
```

```html
result:

xdd.html:14 200
xdd.html:15     <ul>
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
    </ul>
xdd.html:16 OK
xdd.html:17     <ul>
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
    </ul>
xdd.html:18 success
```

