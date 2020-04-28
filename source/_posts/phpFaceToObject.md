---
title: phpFaceToObject1
date: 2019-12-06 19:29:31
tags:
- php
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191207110327.png
---

### 引入php文件

```php
include 'angelina.php';
```

## 构造函数:

两种方法:

```php
function __ construct($name,$sex,$age){}
//
function __ "此类的类名"(...){}
```

## 析构函数

当对象结束其生命周期时,系统会自动执行这个函数

```php
class Person{
    function __destruct
}
```

# 封装

## var 

php中默认将var 关键字解释为public,var等同于public

## public

用public修饰的属性和方法是公开的,在程序的任何位置都可以访问,子类可以继承父类所有的公共成员

## private

private修饰的属性和方法只能在所属类的内部访问,子类也不能继承

```php
//例如现在先定义一个类
  	class Person{
        public $name;
        private $money;
        function __construct(){
            $this->name = "jack";
        }
    }  
//
	$jack = new Person();
	
```

## protected

protected 修饰的属性和方法只有除了子类可以调用外,其他类不能调用,包括在类的外面

```php
<?php
//protect
class Person
{
    public $name;
    public $hello;
    protected $money;
    function __construct()
    {
        $this->name = "angelina";
        $this->age = 12;
        $this->money = 10000;
    }
}

class girl extends Person
{
    public function numOfMoney()
    {
        return $this->money;
    }
}
$ange = new girl();
echo $ange->numOfMoney();//10000
echo $ange->money;//Fatal error: Uncaught Error: Cannot access protected property girl::$money
```

## extend

继承一个类,但不支持多继承

eg如上

## final

> **被final修饰的属性和方法不能被更改,**
>
> **被final关键字修饰的类不能被继承,**
>
> **被final关键字修饰的方法在子类中不能被重写,**
>
> **final不能修饰变量**

## 多态

> **指在面向对象中能够对同一个接口做出不同的实现,主要存在两种形式:**

### 重写

> **在子类中重写父类的方法,具有相同的方法名字,相同的参数表和相同的返回类型,常用于子类构造方法的重写.**

### 重载

> **通常是指同一个类中多个方法具有相同的名字,但这些方法具有不同的参数列表**

```php
<?php
//
class Person
{
    public $name;
    public $birthday;
    function __construct($name, $birthday)
    {
        $this->name = $name;
        $this->birthday = $birthday;
    }
}
$girl = new Person("eyjafjalla", 12);
echo "<pre>";
var_dump($girl);

//输出结果
object(Person)#1 (2) {
  ["name"]=>
  string(10) "eyjafjalla"
  ["birthday"]=>
  int(12)
}
```



## "::"操作符

> **通常用于没有声明任何实例的情况下使用类的属性和方法**

和$this的区别

`parent:: `可以调用父类中的**属性**和**方法**和常量 比如构造函数

`self:: `可以调用本类中的**静态属性**和**方法**和常量

`类名::` 可以调用某类中的**静态属性**和**方法**

👩:可以是非静态的,但是系统不推荐这样做

## static

静态,可以使用 "类名::" 的方式调用.

不需要实例化对象就可以访问或调用,

## abstract

> 抽象类,它是一种不能被实例化的类,必须至少要有一个抽象方法,且抽象方法没有方法体,要连接一个分号,通常需要定义一个子类

```php
abstract class Person(){
    abstract function get_area();
}
```

## 接口

> 用interface关键字来定义,它是一种特殊的抽象类,接口中未实现的方法,即使是空方法,也必须在子类中实现.一个类只能继承一个父类,但是却可以实现多个接口,通过implements 关键字可以实现接口

```js
//interface & implements
interface Work
{
    function getJobSkill();
}
class Programmer implements Work
{
    function getJobSkill()
    {
        return array(
            "java",
            "php",
            "C"
        );
    }
}
$a = new Programmer();
var_dump($a->getJobSkill());
```

