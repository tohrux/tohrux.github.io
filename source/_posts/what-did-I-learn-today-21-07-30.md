---
title: 21-07-30
date: 2021-07-30 19:32:53
tags: diary
---

# 简易双向数据绑定

## 参考

[深入浅出`Object.defineProperty()`](https://www.jianshu.com/p/8fe1382ba135)

```js

<body>
    <input type="text" id="input" />
    <p id="data"></p>
    <script>
        const obj = {};
        const input = document.getElementById('input');
        Object.defineProperty(obj, 'name', {
            get() {
                return input.value;
            },
            set(newVal) {
                input.value = newVal;
                console.log(newVal)
                document.getElementById('data').innerHTML = newVal;
            }
        });
        input.addEventListener('input', () => {
            obj.name = input.value;
        })
        obj.name =  "hello"
    </script>
</body>
```

