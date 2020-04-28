---
title: vue v-text/html/插值表达式/v-bind/v-on
date: 2019-12-25 17:52:04
tags:
- vue 
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos//img/20191224154153.png
---

```html
    <div id="app">
        <p>
            {{msg}}
            <div>hello</div>
        </p>
        <div v-html="msg2"></div>
        <input type="button" v-on:click="show" :value="msg">
    </div>
    <script>
        var vm = new Vue({
            el: '#app', //表示上面new的vue的实例,要控制页面上的哪个区域
            data: { //data属性中存放的是el中要用到的数据
                msg: 'hello,我是msg',
                msg2: '<h1>hello ,I am msg2</h1>',
                btbMsg: 'click me'
            },
            methods: {
                show: function(){
                    alert(123);
                }
            }
        })
    
        
    </script>
```

v-html,v-text:👩

```
v-html,会直接解析data中的字符串里的html标签
两者在使用时,在被绑定的html标签(<div v-html="msg2"></div>中间输入内容是无效的,如果需要输入内容可以使用{{插值表达式}}
```

v-bind:

```
要为非v-开头的属性赋值时且想用datao里的数据可以使用"v-bind:",简写":",👩:可以加上字符串或数字,把data中的属性当作变量使用👇
	:value="btbMsg+123"
```

v-on: Vue提供的事件绑定机制 (简写@ 下面可以直接写成@click='show')

```
<input type="button" v-on:click="show" :value="msg">
需要在Vue里定义method
```

