---
title: phpFaceToObject2
date: 2019-12-09 15:04:11
tags:
- php
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191207110327.png
---

## 对象的使用

### 引用对象

```php
$a = "hello";
$b = &$a;
echo $b . "</br>"; //hello

$a = "aloha";
echo $b; //aloha
```

### 克隆对象

```php
class Person
{
    public $timeForCopy = 0;
    function __clone()
    {
        $this->timeForCopy += 1;
    }
}
$a = new Person();
$b = clone $a;
$c = clone $b;
echo $b->timeForCopy; //1
echo $c->timeForCopy;//2
```

### 比较对象

```php
"===" 表示比较两个对象的内存地址 "=="比较的是两个对象的内容
```

经过比较可以得出:

```php
clone的两个对象相比较的话: 值相等 ,但是内存地址不相等
引用的两个对象: 值和内存地址都是相等的
使用一样的构造函数生成的两个实例化对象: 值是一样的,但是内存地址不同
```

### 检测对象类型

*案例来自php.net*

方法:

```php
instanceof 关键字
```

对两个不同无关的类使用

```php
<?php
class MyClass
{ }
class NotMyClass
{ }
$a = new MyClass;

var_dump($a instanceof MyClass); //true
var_dump($a instanceof NotMyClass);//false
```

对继承后的类使用

```php
<?php
class ParentClass
{ }

class MyClass extends ParentClass
{ }

$a = new MyClass;

var_dump($a instanceof MyClass); //true
var_dump($a instanceof ParentClass);//true
```

接口

```php
<?php
interface MyInterface
{
}

class MyClass implements MyInterface
{
}

$a = new MyClass;

var_dump($a instanceof MyClass);//true
var_dump($a instanceof MyInterface);//true
```

## 魔术方法

"__"开头的方法都被称为魔术方法(属实👍)

比如之前的 \_\_construct() 每次实例化一个类都会先调用该方法进行初始化。

### __set()

在给不可访问属性赋值时，[__set()](https://www.php.net/manual/zh/language.oop5.overloading.php#object.set) 会被调用。

### __get()

public __get ( string `$name` ) : [mixed](https://www.php.net/manual/zh/language.pseudo-types.php#language.types.mixed) 当读取不可访问的属性时,\_\_get()会被调用

### __call()

用来处理程序在调用不存在或私有的方法时所导致的错误(友好)

```php
<?php
class Fruit
{
    function __call($method_name, $param)
    {
        echo $method_name . "方法不存在";
    }
}
$a = new Fruit();
$a->adf(123);//adf方法不存在
```

#### __toString()

👩:只对echo 和 print 有效,可以将对象输出为字符串

输入:

```php
<?php
echo "<pre>";
class Fruit
{
    function __toString()
    {
        return "fruit man";
    }
}
$a = new Fruit();
print($a);
echo "</br>";
echo ($a);
echo "</br>";
var_dump($a);
```

输出:

```php
fruit man
fruit man
object(Fruit)#1 (0) {
}
```

