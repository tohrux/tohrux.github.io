---
title: larave表单验证
date: 2019-11-25 08:26:54
tags:
- php
- laravel
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/laravel1.png
---

# 表单验证:

多个验证规则可以通过"|"隔开:

语法:

```php
$this->validate(数据对象,[数组形式的验证规则])
```

|  规则名   |                             说明                             |
| :-------: | :----------------------------------------------------------: |
|  require  |                           不能为空                           |
| max:value | 字段值必须小于或等于value,如果是字符串 value则为字符串的个数 |
|   email   |                       验证邮箱是否合法                       |
| confirmed | 验证两个字段是否相同,如果是password则必须输入与之匹配的paasword_confirmation字段 |
|    url    |                      字段必须为有效URL                       |
|  integer  |                          必须为整数                          |
|  numeric  |                          必须为数值                          |
|    max    |                         最多255字符                          |
|    min    |                          最少1字符                           |

# 实现用户验证功能

1. 创建一个用户控制器

2. 新建一个index.blade.php页面

3. 引入静态资源 CSS,Js等 

4. 配置路由

5. csrf验证:

   ```php
   {{csrf_token()}}//会在页面显示 纯文本显示 用在异步提交 ajax
   
   {{csrf_field()}}//一般已html元素的形式生成 自动hidden
   👇也可以直接写成这个
       @csrf
   ```

   csrf_field自动生成的html元素:

   ```html
   <input type="hidden" name="_token" value="i4Q2RwjAN5NpYyUwJogKSjsza9VBi4hYtwQ7gvvu">
   ```

   

# 如何得知一个请求类型

```php
 public function index(Request $request)
    {
        echo $request->method();
    }
```

# 验证

```php
//CONTROLLER.PHP:
    public function index(Request $request)
    {
        if ($request->method() == 'POST') {
            echo $request->method();
            $this->validate($request, [
                'name' => 'required|min:2|max:20',
                'password' => 'required|min:6'
            ]);
            echo "success!";
        } else {
            echo $request->method();
            return view('users.index.index');
        }
    }


//INDEX.BLADE.PHP:
    @if(count($errors) > 0)
    <div class="alert alert-danger">
        <ul>
            @foreach ($errors->all() as $error)
                <li>{{ $error }}</li>
            @endforeach
        </ul>
    </div>
    @endif

    <form action="" method="post" >
            <p>usrname<input type="text" name="name"></p>
            <p>password<input type="password" name="password"></p>
            @csrf
            <p><input type="submit"></p>
       </form>
//WEB.PHP
        Route::any('/users/index/adduser', 'UserController@index');
```

## 独立验证实现

```php
$validate = Validator::make($request->all(), [
'name' => 'required|min:2|max:20',
'password' => 'required|min:6'
]);
//打印对象所有的方法 04:fails
dump(get_class_methods($validate));
if ($validate->fails()) {
//通过重定向回退
// return redirect()->back()->withErros($validate);
}
```

## 通过验证器文件来实现

通过命令行创建一个验证器文件

```cmd
php artisan make:request UserRequest
```

然后在该文件进行配置

```php
    public function rules()
    {
        return [
            //编写自定义规则
            'name' => 'required|min:2|max:20',
            'password' => 'required|min:6'
        ];
    }
    //如果需要中文的错误提示,则需要手动写方法
    public function message()
    {
        return [
            'name.requiired' => '不能为空',
            'password.requiired' => '不能为空'

        ];
    }
```



## 关于验证语言包

可以通过这个网站去下载[packagist]

[packagist]: https://packagist.org/packages/caouecs/laravel-lang	"packagist"

使用composer安装完后 再到vendor下拿到这个文件复制到\resources\lang下

再在validation把locale修改为想要的语言就🆗