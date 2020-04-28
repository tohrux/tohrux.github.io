---
title: sass基础语法
date: 2019-11-18 18:31:47
tags: 
- sass
- css
- 前端
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/sass_logo.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/sass_logo.png
---

# 搭建环境

Sass是基于ruby开发的,但是用的人却不用懂得写Ruby.

首先,在编写Sass前要先下载安装Ruby

(在网上搜索Ruby的时候 看到的评价都在说这门语言很优雅,以后有空的话会去接触下的!)

👇

然后在命令行中 输入 

```命令行
gem install sass 
```

等待执行完毕后 然后输入在命令行输入

```c
sass -v
```

如果出现了相应的版本号 就意味着安装成功了👏

# 开始基础语法

## 注释

```scss
/*注释*/ 👈这种注释会在编译后的CSS中显示
//注释   👈这种则不会
```

## 变量

```scss
$变量名字:变量属性值
```

使用! default 会让之前的样式覆盖掉当前的样式

```SCSS
//你好 我是sass

$defaultColor: red;

$defaultColor: #0000ff !default;

h1{color:$defaultColor;}
```

编译后的css:

```css
h1 {
  color: red;
}
```

## 关于变量的作用域

💡需要注意的是如果上述变量的作用域在所有类的外面,那它就是全局变量,否则他的作用域只在当前的类

## 嵌套CSS规则

```scss
/* SASS嵌套 */
$defaultColor: red;
#content{
    article{
        h1{color: $defaultColor;}
        p{color: $defaultColor;}
    }
    aside{
        color: aqua; 
    }
}
```

编译后的css:

```css
#content article h1 {
  color: red;
}

#content article p {
  color: red;
}

#content aside {
  color: aqua;
}
```

## "$"同时也可以代表父元素选择器

```scss
/*sass*/
a{
    font-weight: bold;
    text-decoration: none;
    $:hover{ color:yellow; }
    p.login $ {font:weight:normal}
     
}
```

```css
/*编译后的CSS*/
a{
    font-weight: bold;
    text-decoration: none;
}
a:hover{
        color:yellow;
        }
p.login a {font:weight:normal}
```

## 定义混合指令

如果网站中有很多地方需要部署相似的样式,可以使用@mixin来进行封装

```scss
/*Sass*/
    @mixin large-text {
        font:{
            family: Arial;
            size: 20px;
            weight: bold;
        }
        color: #ff0000;
    }
    p {@include large-text()}
	a {@include large-text()}
```

```css
/*编译后的CSS*/
p {
  font-family: Arial;
  font-size: 20px;
  font-weight: bold;
  color: #ff0000;
}

a {
  font-family: Arial;
  font-size: 20px;
  font-weight: bold;
  color: #ff0000;
}
```

### 使用$指向父类选择器

```scss
/*Sass*/
//@mixin 混合指令  
$xu:#010203;
$w:10px;
@mixin text{
    font:{
       family: 华文宋体;
       weight: bold;
       size: $w*2.5;
    }
    &:hover{
      cursor: pointer;
      text-decoration:underline #a94442 ;
    }
  }
  p{
    //通过@include调用  导入
    @include text;
  }
```

```css
/*编译成CSS*/
p {
  font-family: 华文宋体;
  font-weight: bold;
  font-size: 25px;
}

p:hover {
  cursor: pointer;
  text-decoration: underline #a94442;
}
```

### 通过传参  => 有参函数

(可以给定默认值 例如$width = 1 ,这样在不给参数的时候就会默认显示1)

```scss
/*sass*/  
@mixin myborder($color,$width,$style){
    border:{
      width: $width;
      color: $color;
      style: $style;
    }
 }
 .b{
   //  传参需要一一对应
   @include myborder(red,5px,solid);
 }
```

```css
/*编译成CSS*/
.b {
  border-width: 5px;
  border-color: red;
  border-style: solid;
}
```

### 不确定参数的数量时...

```scss
//  不确定参数的写法
@mixin box-s($shadow...){
    -moz-box-shadow:$shadow;
    box-shadow:$shadow;
    -o-box-shadow: $shadow;
}
.b3{
 //    属性可以省略   参数3不能负数
//           水平阴影 垂直 阴影半径 阴影程度 颜色 Insert内扩
@include box-s(5px 5px 5px 5px #123654);
}
```

```css
/*编译后*/
.b3 {
  -moz-box-shadow: 5px 5px 5px 5px #123654;
  box-shadow: 5px 5px 5px 5px #123654;
  -o-box-shadow: 5px 5px 5px 5px #123654;
}
```

## 运算

### 数字运算

Sass支持 +,-,*,/,%等运算

如果在运算时不给单位的话,则会自动补充单位

```scss
.fon{
    $a:10px;
    $b:10;
    $c:#123456;
                                                                                
    min-width: $a/2;
    max-width: $a*2; 
    margin: (10px/2);//两个数字之间要加括号才可以进行除法运算
    padding: #{$a}/#{$b};//使用#{$a}可以不进行除法运算
}
```

```css
/*编译后的css*/
.fon{min-width:5px;max-width:20px;margin:5px;padding:10px/10}
```

## 字符串运算

```scss
.str {
    $s:"宋体";
    $t:"微软雅黑";
    $r:"sans";
    font-family: $s + $t;
    font-family: $r + "-self";
}
```

```css
/*编译后的CSS*/
.str{
    font-family:"宋体微软雅黑";
    font-family:"sans-self"
}
```

## 条件判断和循环

### 使用@if 和 @else 

(支持and/or/on/not)

```scss
.bol{
    $age:25;
    @if ($age > 18 and $age < 27){
        color: yellow;

    }@else{
        color: green;
    }
}
```

```css
/*编译后的CSS*/
.bol{color:yellow}
```

eg2:

```scss
@mixin block($bol){
    @if($bol){
        dispaly:block;
    }@else{
        display: none;
    }
}
.block{
    @include block(true);
}
.hidden{
    @include block(false);
}
```

```css
/*编译后的css*/
.block {
  dispaly: block;
}

.hidden {
  display: none;
}
```

### @for 循环 

@for $i from <start> through <end> {}(会through最后一个数字)

@for $i from <start> to <end>{} (忽略最后一个数字)

```scss
@for $var from 1 through(或者to) 3 {
    .item-#{$var} {width: 2em * $var;}
}
```

```css
/*编译后的css*/
.item-1 {
  width: 2em;
}

.item-2 {
  width: 4em;
}

.item-3 {
  width: 6em;
}
```

### @each 

@each $example in example1,example2,example3{}

```scss
@each $animal in puma, sea-slug, egret,salamander{
    .#{$animal}-icon{
        background-image: url('image/#{$animal}.png');
    }

}
@each $header, $size in (h1:2em, h2:1.5em, h3:1em){
    #{$header}{
        font-size: $size;
    }
}

```

```css
/*编译后CSS*/
.puma-icon {
  background-image: url("image/puma.png");
}

.sea-slug-icon {
  background-image: url("image/sea-slug.png");
}

.egret-icon {
  background-image: url("image/egret.png");
}

.salamander-icon {
  background-image: url("image/salamander.png");
}

h1 {
  font-size: 2em;
}

h2 {
  font-size: 1.5em;
}

h3 {
  font-size: 1em;
}

```

### @while 

while循环使用指令重复输出格式知道表达式返回结果为false.可以实现比@for循环更为复杂的指令

```scss
$i: 5;
@while $i>0{
    .h#{$i} {
        width: 2em * $i;
        $i : $i - 2;
    }
}
```

```css
.h5 {
  width: 10em;
}

.h3 {
  width: 6em;
}

.h1 {
  width: 2em;
}
```

### 数组

Sass的数组常常被称为"map",它总是以键值对的形式出现--"key:value"

语法格式:

```scss
$map: (
    key1:value1,
    key2: (
        key2-1: value2-1,
        key2-2: value2-2,
    ),
    key3: value3
);
```

例子:

```scss
$some-color:(
    a: #ea4c89,
    b: #3b5998,
     c: #171515
);
.btn-a{
    color:map-get($some-color, a ) //👈这里使用了map-get方法 这是map自带的方法
}
```

```css
/*编译后*/
.btn-a {
  color: #ea4c89;
}
```

### 选择器继承@extend

```scss
.father{
    border: 1px solid black;
}
.son{
    @extend .father;
}
```

```css
.father, .son {
  border: 1px solid black;
}
```

# 最后

终于完成了,😭,虽然有些疲惫.

以上都是基于我的老师@帅帅徐 笔记内容&上课所讲,以及 书(@web前端开发中级 下册) 和自己微不足道的总结,

感谢阅读🙌

2019/11/19

下午 6:47

------

刚刚问了老师一句,"实际开发中会用到sass吗 ?"

然后他回了我一句"你应该反过来问" 😂



