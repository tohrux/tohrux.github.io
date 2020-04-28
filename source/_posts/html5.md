---
title: html5 -private
date: 2019-11-29 18:16:22
tags:
- html
- private
- 前端
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191130141218.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191130141218.png
---

*本文算是一个个人向的笔记,涉及到的都是书上出现过,但是我不怎么熟悉的内容,<s>相当于把书过一下</s>*

*index_img来自斉藤健吾@月曜日 南 ナ26ab (@kengo1212)： https://twitter.com/kengo1212?s=09*

插入个音乐播放器测试一下!

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=454224982&auto=1&height=66"></iframe>


## 一些常用H5标签

```
	<b> bold
    <sub> 下标
    <sup> 上标
    <bdo dir="rtl">123</bdo> 
    <strong> 强调(加粗,会优先使用)
    <em> emphasized
    <i> italic
```

### \<a>

```html
<a href="rikka.png" donwnload="">click here to download</a>
```

**download**标签:加入后点击链接不会跳转,而是直接开始下载

### \<dl>

定义列表dl: 英文全称definition list

```
    <dl>
        <dt>地区</dt>//denifition title
        <dd>上海</dd>//definition description
        <dd>上海</dd>
        <dd>上海</dd>
    </dl>
```

输出:

```html
地区
	上海
	上海
	上海
```

👩如果margin和padding设置为0,则不会有缩进的效果

# 表格元素\<table>

### \<caption>

用于定义表格的标题

### \<th>

```html
    <table>
        <tr>
            <th>1</th>
            <th>2</th>
            <th>3</th>
        </tr>
    </table>
```

### rowspan&colspan

用于合并单元格,直接在`td`中使用

```html
eg:<td rowspan="2">
```

### \<colgroup>

//这标签完全可以用在css中写样式的方式代替

通常在\<table>的下方直接加,与`col`一起使用

```html
        <colgroup>
            <col span="2" width="200">
            <col width="100">
        </colgroup>
```

👆,`span`:\<number>,表示样式被改变的列数,不给值得话默认为1

​	`width`:表示被当前\<col>影响的列的宽度.

​	\<col>:如果第一个\<col>标签的 span=2,那么第二个\<col>标签就会从第三列开始执行.

### html5新增的语义化标签

\<header> \<main> \<footer>

\<article>:只要是单独的文档内容就可以使用

\<session>:用于定义文档中的一个区域,强调分段,分区

👩区别:如果是一段主题性的内容,则用session,如果一段脱离下文仍是完整且独立的存在的一段内容,则用article.两者可以互相嵌套.

`<aside>`:用于定义与文章内容无关的附属信息,通常用于嵌入内容和侧边栏.

`<nav>`:导航栏

### \<meter>&\<progress>

进度条.

可选值 `max`  `min`  `value`  //没有作进一步的了解

### \<frameset>

框架的集合

### \<video>&\<audio>

可以添加`controls`来添加控件,

## contenteditable

如果该属性的值设置为true,则允许用户直接修改页面上的元素

例如可以在\<table>,\<div>中添加此元素

但是刷新后修改的内容就会丢失

👩`designMode` ,这个属性可以在在js修改.相当于全局的 contentedittable

```js
document.designMode = "on";
```



## hidden

html5所有的元素都有hidden属性,hidden="true" 相当于 dispaly="none"

//onclick里可以直接添加js内容👇

```html
    <button id="button" onclick="
        var target = document.getElementById('target');
        target.hidden = !target.hidden;
        var button = document.getElementById('button');
        if(target.hidden){button.innerHTML='show'}else{button.innerHTML='hidden'}
    ">show</button>
    <div id="target" hidden="true">
        say what?
	</div>
```



# 表单元素\<form>

在需要上传时,`enctype`的值需要改为 `multipart/form-data`

`name`的值的设置一般要与`id`的相同

# 表单控件

## \<input>

可选值

- week
- month
- color
- date
- month
- date
- time
- url 移动端
- tel 移动端
- search 移动端
- range -拖动条

属性:`maxlength` `readonly` `disable`

## \<label>

有两种用法:

```html
    <label>
        nihao
        <input type="text" id="hello">
    </label>
2> 
	<label for="hello">
        nihao
        <input type="text" id="hello">
    </label>
```

## \<select> 

```html
select
```



## \<button>

type =`  button` / `submit`/ `reset`

## formaction

当你不需要一次提交整个form中的数据时,可以在`submit`中使用这个属性

formaction = "你需要提交的id值"

```html
    <form action="" method="get">
        <input type="text" id="username" name="username">
        <input type="password" id="password" name="password">
        <input type="submit" formaction="username">
        <input type="submit" formaction="password">
    </form>
```

👩 `formmethod`/ `formenctype` / `formtarget` 同理

## autocomplete/autofocus

autocomplete为自动填充,

autofocus,当你为某个`input`添加这个元素时,打开页面的同时这个`input`会获取焦点.

## list

建议和`datalist`一起使用 eg:

```html
    <form action="" method="get">
        <label>
            <input type="text" list="location" placeholder="waifu">
        </label>
    </form>
    <datalist id="location">
        <option value="angelina">安洁莉娜</option>
        <option value="Eyjafjalla">艾雅法拉</option>
        <option value="chen">陈</option>
    </datalist>
```

效果还挺炫:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191129194042.png)输入为空时

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191129194106.png)输入一个'a'

### patter

用于给当前的`input`加入验证,(正则表达式)

eg:

```html
    <form action="">
        <input type="text" name="" id="" pattern="[0-9]*">
        <input type="submit">
    </form>
```

## novalidate

在表单内加入这个属性,就可以避免验证直接提交

👩`form`标签,`input`标签都可以使用

```html
<form action="" novalidate="novalidate">
		<input type="email" name="user_email" />
  		<input type="submit" />
</form>
```



### required

规定必须要填入内容,否则无法提交

```html
<input type="text" name="usr_name" required="required" />
```

