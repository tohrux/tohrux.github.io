---
title: jQ -private
date: 2019-12-03 08:15:03
tags:
- jQuery
- javascript
- 前端
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191203123227.png
---

## 测试是否引入成功

```js
$(document).ready(function(){
    alert('ohiyo~');
})
```

## 语法

- $(this).hide();
- $("p").hide(); //hide所有的p元素
- $("p.test").hide(); //hide所有class=test 的p元素

## 入口函数

### jQ

```js
$(function(){
    
})

$(document).ready(function(){
    
})
```

### JS

```html
window.onload(function(){
	
})
```

### 区别:

`$(document).ready(funtion(){})` : 等HTML所有标签(DOM)都加载完才执行

`window.onload(function(){})`: 等所有内容都加载完,包括外部的图片,才执行

## JQ选择器

### 属性选择器

`$("element[attribute]")`

```javascript
eg:
$("div[titles=test]").css(5px solid red);//titles = 'test' 的所有div
$("[title^=ohiyo]")//以'ohiyo'开头
$("[title$=ohiyo]")//以'ohiyo'结尾
$("[title*=ohiyo]")//包含'ohiyo'
```

### 位置选择器

`$("element:position")`

```js
eg:
$("button[class=ohiyo]:first") // 表示class = 'ohiyo' 的第一个button
可选值
:last
:odd //奇数
:even //偶数 👩:0也算是哦,baby~
:eq(n)
:gt(n) //Greater Than 大于 
:lt(n) //Less Than 小于
👩:这里要注意,gt是一个段落筛选,从指定索引的下一个开始,例如gt(1)代表从大于索引为1的的选择器,所以它是从2开始的
```

额外选择器:

- next()

- prev()

- nextAll()

- prevAll()

- siblings()

  

### 多选择器的写法

`$("[title*=ohiyo]:eq(0),[title*=ohiyo]:eq(1)")`

后代 ,子代, id  ,类 ,标记, 略

### 一些个人的eeeee

关于eq()的一些问题

```html
<body>
    <ul class="navi">
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
        <li>nihao</li>
    </ul>
    <ul class="navi">
        <li>hei</li>
        <li>hie</li>
        <li>hie</li>
        <li>hie</li>
        <li>hie</li>
    </ul>
</body>
<script>
    $("ul.navi li:eq(3)").css("background","red");
</script>
👩:这里的li中只有第一个ul的第四个li才会变red
👨:那如果我想让每个ul的第四个li变red要怎么做?
👩:那你可以这写:
	$("ul.navi").each(function(){
    	$(this).find("li:eq(3)").css("color","red");
    });
👨:我佛了,那么复杂?给👴爬
👩:那宁可以这样✍:
	$("ul.navi li:nth-child(4)").css("color","red");
```



### 选择器对象

```html
	$("ul.navi").each(function(){
    	$(this).find("li:eq(3)").css("color","red");
    });
```

## 创建和添加html元素

```js
    $btn = $("button");
    $btn.click(function () {
        var $li = $("<li>我爱这个世界</li>");
        $("ul[title=first_title]").append($li);
    });
```

### append()

### apendTo()

### prepend()

### prependTo()

### after()

### before()

## 删除元素

### remove()

它的效果是将元素删除,**包括它的后代**

### empty()

它的效果是删除该元素的后代删除,**但是不会删除自己本身**

👩括号中的参数可以是node,dom,$对象



## Dom对象和jQ对象互相转换

Dom -> JQ

`$(document.getElementById("hi"))`

jQ -> Dom

`$(document.querySelector("span")).get(0)`

`$(document.querySelector("span"))[0]`

