---
title: bs
date: 2019-12-13 10:31:41
tags:
- bootstrap
- css
---

# 媒体对象

```html
//媒体对象 container>row>col>media>img + media body //<-放文字

    <div class="container bg-danger">
        <div class="row justify-content-center">
            <div class="col-6 bg-info">
                <div class=" media">
                    <img class="align-self-center" src="ark/pzw.png" alt="">
                    <div class="media-body">
                        <h5 class="mb-0">Header</h5>
                        Content
                    </div>
                </div>
            </div>
        </div>
    </div>
```

# text

- text-align
- text-center
- text-right
- text-nowrap
- text-justify //针对西文字体,可以让字体的间隔,尽量使左右侧都对齐
- text-lowercase
- text-uppercase
- text-capitalize 
- *text-primary/dark/info...

# 列表

```html
ul>li ol>li dl>dt>dd
*ul/ol/dl
```

- list-unstyle 加在ul中  可以清除 但是依旧会保留ul的margin
- list-inline 清除ul所有的样式
- list-inline-item 加在每个li中 使他们变成行内元素

```html
    <ol class="list-inline">
        <li class="list-inline-item">123</li>
        <li class="list-inline-item">123</li>
        <li class="list-inline-item">123</li>
    </ol>
```

# 表格

- table 每行增加水平分割线以及少量padding,最重要的是会变成响应式布局
- table-responsive 会在小屏幕上出现滚动条
- table-hover
- table-striped
- table-bordered
- table-hover

# 图片

- img-thumbnail

  

# 表单

- .form-inline
- .form-group
- .form-control 
- .form-group-lg/sm
- .input-lg/sm
- .checkbox 
- .radio 

```html
<div class="form-inline ">
        <div class="form-group">
            <label for="password">pass</label>
            <input type="password" id="password" class="form-control">
        </div>
        <div class="form-group">
            <label for="text">lOGiN</label>
            <input type="text" id="text" class="form-control">
        </div>
</div>
```

# 按钮

- .btn
- .btn-primary/success/info......
- .btn-lg/sm/xs 
- .btn-block ->块级按钮,会填满整个父容器
- .active ->被选中样式
- .disable -> 不可用
- .focus -> 获取焦点的样式
- btn-group (-vertical)
- btn-toobar

# 下拉菜单

- .dropup/down 容器 
- .dropdown-menu 
- .dropdown-item
- .dropdown-toggle -> 箭头小图标
- data-toggle -> 表示医生们进行触发
- btn-group ->使按钮的间距为0

*下拉注册

```html
    <div class="dropdown btn-group">
        <a href="" class="btn btn-danger dropdown-toggle" data-toggle="dropdown"></a>
        <button class="btn btn-danger">about</button>
        <button class="btn btn-danger">about</button>

        <div class="dropdown-menu p-0">
            <form action="">
                <div class=" input-group">
                    <input type="text" class=" form-control" id="kk">
                </div>
                <div class=" input-group">
                    <input type="text" class=" form-control">
                </div>
                <div class=" dropdown-divider"></div>
                <div class="row justify-content-center align-content-center">
                    <a href="" class="btn btn-dark text-center ">log in</a>
                </div>
            </form>
        </div>
```

## 输入框组

```html
    <div class="container">
        <form action="">
            <div class=" input-group ">
                <div class=" input-group-prepend">
                    <span class="input-group-text">@</span>
                </div>
                <input class=" form-control" type="text" placeholder="aloah">
            </div>
        </form>
    </div>
```

```html
input-group>(input-group-prepend>input-group-text)+(input)
```

- .input-group-prepend/append
- .input-group-text
- .input-group

# nav

- navbar
- navbar-light/dark ->修改字体颜色(nav brand)
- navbar-brand ->  brand
- nav-justified -> 按比例分配空间
- nav-fill 等比分配空间
- navbar-form
- navbar- link
- navbar-btn
- navbar-text
- navbar-left/right
- navbar-fixed-bottom
- navbar-fixed-top
- navbar-static-top



# 分页

- pagination

  

# 面包屑导航

```html
 <ul class=" breadcrumb">
        <li class=" breadcrumb-item"><a href="">
                hi
            </a></li>
        <li class=" breadcrumb-item"><a href="">
                hey
            </a></li>
    </ul>
```

# 标签

- label

徽章

- badge

```html
    <span>hello</span>
    <span class=" badge badge-danger">123</span>
```

# 缩略图 v3

- thumbnail

- caption

  ```html
   <div class=" thumbnail">
          <img src="" alt="">
          <div class=" caption">
              <h5></h5>
              <button></button>
              <button></button>
          </div>
      </div>
  ```

# 警告框

- alert -success/info/warnng....
- alert-dismissable `<可关闭的提示框>`

```html
    <div class=" alert alert-dismissible alert-primary">
        don't be sad
        <button class="close" data-dismiss="alert">
            &times;
        </button>
    </div>
```

# 进度条

```html
    <div class=" progress">
        <div class=" progress-bar" style="width: 10%;">
            <span>10%</span>
        </div>
    </div>
```

# 巨幕

- jumbotron

# 列表组

- list-group

- list-group-item

  ```html
      <ul class=" list-group bg-info">
          <li class=" list-group-item">123</li>
          <li class=" list-group-item">123</li>
          <li class=" list-group-item">123</li>
          <li class=" list-group-item ">
              kl
              <span class=" badge-danger">
                  123
              </span>
          </li>
      </ul>
  ```



# 字体图标v3

gliphicon 



# 之前的一些笔记

### 直接给col 而不是 col-1,2,3可以自动分配剩下的空间

### 可变宽度内容: col-{breakpoint}-auto

### 在BS中flex

1. align-items-start
2. align-self-start
3. justify-content-start

### 一列超过12行的话会自动跳到下一行

### order

```js
order:1 order:2
```



### offset 

通过marginleft实现,后面的元素会跟着移动

修改默认的md,lg等大小

```html
$grid-breakpoint:()
	xs: 420px,
	sm: 768px,
	.....
;
```

### 

```html
<small></small>
<mark></mark>
<abbr></abbr>
<blockquote>
</blockquote>
```

### w-25 h-25 

整体的25%

## x,y,m,p

x:lr

y:tb;

### size(rem)

- 1:0.25;
- 2:0.5;
- 3: 1.0 rem
- 4: 1.5 rem
- 5: 3.0 rem
- 6:auto 自动计算