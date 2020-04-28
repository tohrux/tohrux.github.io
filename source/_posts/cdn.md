---
title: 使用CDN来加速网页的访问
date: 2019-11-17 03:21:58
tags: [build]
index_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/cdn.png
banner_img: https://cdn.jsdelivr.net/gh/tohrux/photos/img/cdn.png
---

# 前言

今天是搭建github.io的第二天,很多功能都还在完善,比如说在一些地方(没错,说的就是你,天朝!)访问GitHub.Page很慢的问题,通过上网一番查找发现似乎可以用CDN来解决.



# 什么是CDN?

这里粘贴一段阿里云官网上面对CDN的描述:

> 将源站内容分发至最接近用户的节点，使用户可就近取得所需内容，提高用户访问的响应速度和成功率。
> 解决因分布、带宽、服务器性能带来的访问延迟问题，适用于站点加速、点播、直播等场景。

总之它可以让别人访问自己的GitHub.Page的速度更快就对了!

# 开始

这里就拿我们网页中需要加载很久的图片来举例8,

首先我们要找到放置自己github.io 页面的那个repo,如下图所示:

![](/img/cdn2.png)

我们需要的图片他们现在都静静的躺在img那个文件夹里

如果想用CDN获取他们的话

可以点击图片最顶端的release来发布版本

例如我这里发布的版本为1.0  发布完成后我们就可通过jsDelivr来引用我们的资源了

![](/img/cdn1.png)

如上面的地址所示:

​	gh 代表 github

​	tohrux是我的GitHub用户名

​	tohrux.github.io是我仓库的名字

​	1.0 是版本号

​	img/fullVersionxx.jpg 是想要获取的文件

> https://cdn.jsdelivr.net/gh/tohrux/tohrux.github.io@1.0//img/fullVersionxx.jpg

然后用这个外链来替换掉你想要替换的文件就大功告成了~

同理,用CDN来引入网页中jQuery,bootstrap等文件也是很常用的做法哦

## 最后

这算是第一次写博文8,其实就是把今晚的问题解决了,然后再总结一下,站在巨人的肩膀上真的很爽啊😊(憨憨笑)

说实话我也不知道CDN到底有没有带来显著的效果,不过欢迎在下方的评论区留言告诉我网页的加载速度有没有变化,感谢阅读!

​			

------

2019/11/17日更新:

​	👇新发现!其实可以用github + jsDelivr + picgo 更方便快捷地实现图片的插入	

> ​		https://github.com/Molunerfinn/PicGo/releases 
>
> ​		[picgo]

[picgo]: https://github.com/Molunerfinn/PicGo	"picgo地址"

