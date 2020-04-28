---
title: flex布局
tags:
- css
- flex
- 前端
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127121638.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127121638.png
---

发现很多地方都会用上Flex布局,所以就决定今晚把Flex给整活了,冲冲冲🐛

在看了一些博客后决定结合自己的理解写下一些笔记

参照：

> https://juejin.im/post/5ddc78f851882573520fb199  作者：**锐玩道**

> https://www.jianshu.com/p/4b14a7a1c6cc                  作者：**sxfshdf**
>
> https://blog.csdn.net/m0_37058714/article/details/80765562 	作者 **wxk_前端开发**
>
> http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html  作者: **阮一峰**

# 一些概念

首先使用Flex布局一定要知道的一点是,这种布局总是以父子的形式存在,父级元素被称为 **容器**(container),有些地方也会称为**弹性盒**,而所有的子级元素会自动地成为这个**容器**的成员,成为 Flex项目(item)

在下文会用 **container** 表示容器, **item**表示Flex项目

```html
display:flex
//当一个元素的display被设置为flex后，它就会成为一个 *container
```

> :hand:这里需要注意的是一旦一个元素被设置为display：flex，子元素的 float,clear,vertical-align将会失效

# **主轴**（main axis )& **副轴**/侧轴(cross axis)

**container**中默认会存在这两条轴，

一般来说，主轴是指水平方向的轴，而副轴是指垂直方向的轴,但是却不是绝对的,比如说下面的这个`flex-direction`属性就可以决定主轴的方向👇

# flex-direction

这个属性决定的是主轴的方向 ,即item们的排列方式

一共有 4个值 分别为 **row** | **row-reverse** | **column** | **column-reverse**; 

```html
.container{
	display: flex;
	flex-direction:  row | row-reverse | column | column-reverse;
}
```

在demo中，我的初始代码如下：

```html
//css部分
<style>
        * {
            padding: 0;
            margin: 0;
        }

        .container {
            display: flex;
            flex-direction: row;
        }

        .container>div {
            width: 100px;
            height: 100px;
        }

        .item1 {
            background-color: red;
        }

        .item2 {
            background-color: yellow;
        }

        .item3 {
            background-color: blue;
        }
    </style>
----------------------------------------------------------------------------------

//body部分
	<body>
    <div class="container">
        <div class="item1"></div>
        <div class="item2"></div>
        <div class="item3"></div>
    </div>
</body>
```

现在分别展示4种 **flex-direction**的效果 :

👩要注意的是，在我的代码中**container**默认宽度是整个**body**的宽度,而高度则内容物(分别是红,黄,蓝三个盒子)而确定.

### row :从左向右排列

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_a1.png)

### row-reverse:从右向左排列

👩这种布局中,并不是单纯地将三个盒子调转了顺序,而是还加了一步:把**item**全都在**container**中从右向左排列.

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_a2.png)

### column:从上到下排列

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_a3.png)

### column-reverse:从下到上排列

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_a4.png)

# flex-wrap

这个属性定义的是,如果在一条水平线上已经存在了过多的**item**(意思就是挤不下了),这些**item**将如何换行.

这个属性有3个值:

```html
.container{
	display: flex;
	flex-wrap: nowrap | wrap | wrap-reverse;
}
```

在demo中我的初始代码如下:

```html
css部分
-----------------------------------------------------------------------------------------
<style>
        * {
            padding: 0;
            margin: 0;
        }

        .container {
            display: flex;
            flex-direction: row;
            flex-wrap: nowrap;
        }

        .container>div {
            width: 100px;
            height: 100px;
            border: 1px solid black;
        }
body部分
-----------------------------------------------------------------------------------------
    <body>
    <div class="container">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
    </div>
</body>
```



下面来看看效果吧:

### 默认效果:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_b1.png)

### **nowrap**:不换行

现在我减小了浏览器窗口的宽度👇

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_b2.png)

再缩小:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_b3.png)

👨hey!!我似乎发现了华点!这就是 **弹性布局**这个名字的由来吗?👆



### wrap:换行

减小浏览器的宽度:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_b4.png)

再减小:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_b5.png)

### wrap-reverse:颠倒顺序的换行方式

减小浏览器的宽度:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_b6.png)

再减小:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_b7.png)

👩可以看到wrap-reverse和wrap中的item顺序是完全反过来的

# flex-flow

这个属性就不多说辣,他的作用是将上面两个属性 **flex-direction** ,**flex-wrap** 写在一行,属于一种简写形式

```html
.container{
	flex-flow:<flex-direction> <flex-wrap> ;
}
```

比如说:

```html
.container {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap-reverse;
        }
```

👇👆效果完全一样

```html
.container {
            display: flex;
            flex-flow: nowrap row;
        }
```

👩tips:这里 **flex-direction** **flex-wrap** 这两个值的顺序是可以调换的

# justify-content

这个属性可以设置item们在主轴上的排列方式

```html
.container{
	justify-content: flex-start | flex-end | center | space-between | space-around
	//常用的有这5个值
}
```



这是我的初始代码:

```html
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .container {
            display: flex;
            flex-flow: nowrap row;
            justify-content: flex-start;
            background-color: #0080ff;
            height: 150px;

        }

        .container>div {
            width: 100px;
            height: 100px;
            border: 1px solid black;
        }

        .item1 {
            background-color: #a3daff;
        }

        .item2 {
            background-color: #1ec0ff;
            width: 200px !important;
        }
    </style>
</head>

<body>
    <div>flex-start</div>
    <div class="container">
        <div class="item1">1</div>
        <div class="item2">2</div>
        <div class="item1">3</div>
        <div class="item1">4</div>
    </div>
</body>
```

👩这里设置了一个`item2`,它的样子与众不同,已此来形成对比

### flex-start

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127105724.png)

### flex-end

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/flex_justify_content_end.png)

### center

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127114926.png)



### space-between

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127114600.png)

### space-around

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127114814.png)

👩注意:`space-around`和`space-between`的区别是:`space-around`会在浏览器窗口内的左右两边生成空隙,空隙的`width`=1/2相邻`item`的间距

# align-items

这个属性可以设置`item`们在副轴上的排列方式,一共有5个可选值

```html
align-item: flex-start | flex-end | center | baseline | stretch;
```

效果如下:

### flex-start:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127124701.png)

### flex-end:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127124750.png)

### center:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127124852.png)

### baseline:

​	![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127130434.png)

👩此处我为每个`item`都设置了 `line-height`=`height`,可以看到 **baseline**的对齐方式很特别,是以文字的基线作为标准的,我觉得可以用来做一些视觉设计.

### stretch

待续

# align-content

设置`container`的中`item`们垂直方向上的对齐方式

```html
align-content: flex-start | flex-end | center | stretch | spave-between | space-around
```

### center

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127140350.png)



### flex-start

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127140505.png)



### flex-end

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127140728.png)



### stretch

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127140909.png)

👩这里的话`stretch`的效果是把整个`container`除去内容后剩余的高度平均分配成行间距,有一点需要说明一下:第一行是会顶到顶部的,而最后一行下面会留下行间距. 大家可以和 `align-content: flex-start`进行对比哦

### space-between

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127142848.png)

### space-around

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127142802.png)

👩看到这里大家在心里会有个疑惑吧,`align-item`和`align-content`的区别是什么呢,其实这是我现在内心中的问号,于是我写下了这篇👇

> https://tohrux.github.io/2019/11/27/flex2/

# `item`上的属性

### order

可以为`item`加上order属性,来改变`item`们的顺序,order值越大的会排在越前面.

```css
//语法
.item1{order = 2};
.item2{order = 1};
```

原本默认的顺序(未加上order属性时):

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191128192154.png)

加上上面代码块的默认属性后:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191128103407.png)



### flex-grow

可以设置`item`的扩展比率,根据所给予的数字大小来分配剩余空间(`width`).

**分配空间的计算方式**:

> 例如整个container的宽度为1000px,现在有三个item在其中,item1的宽度为100px,item2的宽度为200px,item3的宽度为300px,现在container内剩余的宽度为1000px-600px = 400px,现在给三个item分别给与flex-grow属性,item1:0; item2:3; item3:1;现在container将不会有剩余空间,item1的宽度依旧为100,item2则为3/(3+1)\*400+200=500px,item3的宽度为1/(3+1)\*400+300=400px;

👩小tips:如果在container存在一堆item,只要为其中一个赋予flex-grow的值(可以是任何数字)它就会把剩余的空间都占用;

👨tips2:flex-grow的值可以为小数;

### flex-basis

这个元素可以定义`item`的宽度,同时我们知道`width`也可以定义元素的宽度,但`flex-basis`会覆盖`width`的值.

### flex-shrink&flex-basis&flex-grow

关于这三剑客,我推荐大家到这个blog看一下,讲得真的很通俗易懂,很棒,原本是抱着学习的心态去看,看完后发现自己写完全没有意义了

https://blog.csdn.net/m0_37058714/article/details/80765562

作者 **wxk_前端开发**

### align-self

这个属性可以单独定义`item`在 **cross axis** 上的属性,并且可以覆盖`align-item`的属性,前五个值和之前的`align-item`用法一样,如果不给值,则默认给`auto`,表示继承 `align-item`,如果`align-item`也没有给值,则默认值为`flex-start`.

```css
.item {
  align-self: flex-start | flex-end | center | baseline | stretch | auto ;
}
```



未来可能会回来更新,因为到目前为止都只是把案例打了一遍,实际运用中遇到的问题,会记录下来,感谢在互联网上分享知识的人们,i了i了.

关于一些实际运用可以参考阮一峰老师的这篇博文:

http://www.ruanyifeng.com/blog/2015/07/flex-examples.html

























