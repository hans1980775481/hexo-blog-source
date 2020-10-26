---
title: Hexo-评论系统插件
summary: 介绍Hexo如何使用评论系统，完成评论功能
tags:
  - hexo
  - 评论系统
categories:
  - hexo博客搭建
date: 2020-10-25 23:40:27
img:
---

---



> 本文，我们主要来讨论一下，如何使用Hexo系统在[hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)主题下，完成评论功能使用。
>
> [hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)支持多种评论插件的搭配使用：[Gitalk](https://gitalk.github.io/)、[Gitment](https://imsun.github.io/gitment/)、[Valine](https://valine.js.org/) 和 [Disqus](https://disqus.com/) 评论模块（推荐使用 `Gitalk`）
>
> 本篇博客中主要讨论使用Valine的评论系统来完成，评论功能的使用。



### 1. 注册账号

[leancloud官网](https://www.leancloud.cn/)需要现先在官网注册一个账户

### 2. 创建应用

> 注册完账号之后，创建一个用于评论数据的应用

![image-20201025235952054](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201025235952054.png)



> 应用创建好以后，进入刚刚创建的应用，选择左下角的`设置`>`应用Key`，然后就能看到你的`APP ID`和`APP Key`了：

![image-20201026000038758](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026000038758.png)

### 3. 安全域名

为了你的数据安全，请设置自己的`安全域名`：

![image-20201026000559211](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026000559211.png)

### 4. 域名配置

> 由于我们创建的这个应用，使用的是Leancloud配置的默认域名，只有3个月的使用期限，我们可以看到如下提示：

![image-20201026001514066](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026001514066.png)

> 所以我们尽量，为这个应用配置一个我们自己的域名

![image-20201026001620151](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026001620151.png)

![image-20201026001957169](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026001957169.png)

![image-20201026002111146](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026002111146.png)





### 5. hexo配置使用

> 完成数据应用的配置之后，就可以在[hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)的主题配置文件下，编辑`_config.yml`文件中的Valine配置

![image-20201026000946659](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026000946659.png)

> `appId`和`appKey`要和数据应用中的一致，然后，在Hexo博客的更目录下执行`hexo clean && hexo g && hexo s`，访问`http://localhost:4000`然后选择一篇文章，即可看到文章底部有评论界面。

![image-20201026001303572](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201026001303572.png)



> hint: 如果Leancloud的应用太久没用的话，会被archive，我们登陆LeanCloud重新激活应用即可。



***相关链接***

- [Valine 介绍](https://valine.js.org/quickstart.html)
- [hexo博客评论新神器——Valine](https://juejin.im/entry/6844903683356885000)
- [Valine的错误信息](https://dev66.xyz/2020/01/valine-error.html)
- [使用gittalk实现hexo博客评论功能| Jacky Cheng](https://cjjkkk.github.io/gitalk/)

