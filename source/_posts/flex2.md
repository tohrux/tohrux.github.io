---
title: flex布局中 align-items和align-content
date: 2019-11-27 14:36:22
tags:
- flex
- css
- 前端
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191128191207.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191128191207.png

---

### 首先先给出我当前的CSS和HTML

```html
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .container {
            display: flex;
            flex-wrap: wrap;
            flex-direction: row;
            justify-content: space-between;
            align-items: flex-start;
            align-content: space-between;
            background-color: #0080ff;
            height: 700px;

        }

        .container>div {
            width: 100px;
            height: 100px;
            /* border: 1px solid black; */
        }

        .item1 {
            background-color: #a3daff;
            line-height: 100px;
            /* font-size: 120px; */
        }

        .item2 {
            background-color: #1ec0ff;
            width: 200px !important;
            height: 130px !important;
            font-size: 100px;
            line-height: 130px;
        }

        .item3 {
            background-color: #FBFFB9;

        }
    </style>
</head>

<body>
    <div></div>
    <div class="container">
        <div class="item1">1</div>
        <div class="item2">2</div>
        <div class="item1">3</div>
        <div class="item1">4</div>
        <div class="item1">5</div>
        <div class="item2">6</div>
        <div class="item1">7</div>
        <div class="item1">8</div>
        <div class="item1">9</div>
        <div class="item2">10</div>
        <div class="item1">11</div>
        <div class="item1">12</div>
        <div class="item1">13</div>
        <div class="item2">14</div>
        <div class="item1">15</div>
        <div class="item1">16</div>
    </div>
</body>
```

### 👩这里我同时给了`align-item`和`align-content`的值

```css
align-items: flex-start;
align-content: space-between;
```

呈现如下:



<img src="https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127150714.png" style="zoom:67%;" />

可以看到,`align-item`只在每一行中起效果,即在每行中所有的`item`都会顶到当前行的最上方

### 👩再给他们换别的值

现在我把他们修改为,并调整了窗口的大小:

```css
align-items: flex-end;
align-content: flex-start;
```

呈现如下:

![](https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127151648.png)

可以看到`align-content`作用于整个`container`,而`align-item`则作用于他自己那行,和之前的结论一样,<s>好像这段没有必要的样子</s>

### 👨注释掉align-content

```css
align-items: flex-end;
/* align-content: flex-start; */
```

这次我把`align-content`给注释掉了,并且修改了窗口大小,呈现如下:

<img src="https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127161505.png" style="zoom:67%;" />

### 👴给align-content: flex-end;

```css
align-items: flex-end;
align-content: flex-end;
```

这次给了`align-content`值,同样为`flex-end`

<img src="https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127162559.png" style="zoom:67%;" />

我们可以看到在全局下(指`container`) ,每一行的间距已经变成了0.

### 👵将align-item注释掉

```css
/* align-items: flex-end; */
align-content: flex-end;
```

<img src="https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127163124.png" style="zoom: 67%;" />

这里的`align-item`的value已经成为了默认值`flex-start`了

### 结论

`align-item`只作用于每一行的行本身,而`align-content`则作用于全`container`;如果只给`align-item`值,则在全局的每一行间都会有一段默认的不为0的距离,👈这是她的兼职工作,同时`align-item`也会完成她的本分工作:在每一行设置`item`水平排列方式;如果在这时加入个专门做调整全局(`container`)布局的`align-content`的话,`align-item`的兼职工作就会被接过.此时,`align-content`仿佛在对`align-item`说,"你就是`align-item`吗?感谢你之前做的一切,从现在开始请不要担♥任何事,因为我来了!".然后留下`align-item`在原地露出迷妹般的星星眼.

<img src="https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191127165804.gif" style="zoom: 150%;" />



### that's all!