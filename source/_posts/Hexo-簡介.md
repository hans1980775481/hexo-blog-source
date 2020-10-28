---
title: Hexo--簡介
author: xmhans
tags:
  - hexo
categories:
  - hexo博客搭建
date: 2020-10-28 22:58:30
top:
summary: HEXO 簡略説明
img:
---

### 1. Hexo生成界面原理

> 本節主要講述，Hexo怎麽生成界面的，我們寫的明明是Markdown文件爲什麽就可以變成HTML文件呢？以及MarkDown文件生成的HTML文件的對應關係是怎樣的呢？

> 首先我們來看一下，Hexo的文件目錄：
>
> - `node_modules:` 依赖包
> - `public：`存放生成的页面
> - `scaffolds：`生成文章的一些模板
> - `source：`用来存放你的文章
> - `themes：`主题**
> - `_config.yml:` 博客的配置文件**

输入`hexo new post "article title"` 或者 `hexo n "article title"`，新建一篇文章。

然后打开`\source\_posts`的目录，可以发现下面多了一个文件夹和一个`.md`文件，一个用来存放你的图片等数据，另一个就是你的文章文件啦。
你可以会直接在`vscode`里面编写`markdown`文件，可以实时预览，也可以用用其他编辑`md`文件的软件的工具编写。

编写完markdown文件后，根目录下输入`hexo g`生成静态网页，生成的靜態網頁均保存在`public`目錄下。

我們在`source`文件夾下的文件均會被編譯，到`public`文件夾下生成對應的`HTML`文件，`post`中的文件會在`public`文件夾中生成和文章時間一直的目錄最後會有如下目錄：

![image-20201028231554092](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201028231554092.png)

文章的内容會保存在`index.html`文件中



#### 1.2.4 layout（布局）

------

##### **1.2.4.1 post**

当你每一次使用代码

```bash
hexo new XXX
```

它其实默认使用的是`post`这个布局，也就是在`source`文件夹下的`_post`里面。

`Hexo`有三种默认布局：`post`、`page`和`draft`，它们分别对应不同的路径，而您自定义的其他布局和`post`相同，都将储存到`source/_posts`文件夹。

而new这个命令其实是：

```bash
hexo new [layout] <title>
```

只不过这个`layout`默认是`post`罢了。

##### **1.2.4.2 page**

如果你想另起一页，那么可以使用

```bash
hexo new page newpage
```

系统会自动给你在`source`文件夹下创建一个`newpage`文件夹，以及`newpage`文件夹中的`index.md`，这样你访问的`newpage`对应的链接就是http://xxx.xxx/newpage

> 最終使用hexo g 生成界面時，就會生成`newpage/index.html`，如下：
>
> hexo new page "about"

![image-20201028232032913](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201028232032913.png)



##### **1.2.4.3 draft**

`draft`是草稿的意思，也就是你如果想写文章，又不希望被看到，那么可以

```bash
hexo new draft newdraft
```

这样会在`source/_draft`中新建一个`newdraft.md`文件，如果你的草稿文件写的过程中，想要预览一下，那么可以使用

```bash
hexo server --draft
```

在本地端口中开启服务预览。

如果你的草稿文件写完了，想要发表到`post`中，

```bash
hexo publish draft newdraft
```

就会自动把`newdraft.md`发送到`post`中。



#### 1.2.3 Front-matter

> `scaffolds：`生成文章的一些模板

![image-20201028232230247](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20201028232230247.png)

> - `draft.md`: 生成草稿文件的模板
> - `page.md`: 生成頁面文件的模板
> - `post.md`: 生成文章文件的模板

------

`Front-matter` 是`md`文件最上方以 `---`分隔的区域，用于指定个别文件的变量，举例来说：

```
title: Hexo+Github博客搭建记录
date: 2019-08-10 21:44:44
```

下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

参数描述`layout`布局`title`标题`date`建立日期`updated`更新日期`comments`开启文章的评论功能`tags`标签（不适用于分页）`categories`分类（不适用于分页）`permalink`覆盖文章网址

其中，分类和标签需要区别一下，分类具有顺序性和层次性，也就是说`Foo`，`Bar`不等于`Bar`，`Foo`；而标签没有顺序和层次。

```yml
---
title: Hexo+Github博客搭建记录
date: 2019-08-10 21:44:44
author: 洪卫
img: /medias/banner/7.jpg
coverImg: /medias/banner/7.jpg
top: true
cover: true
toc: true
password: 5f15b28ffe43f8be4f239bdd9b69af9d80dbafcb20a5f0df5d1677a120ae9110
mathjax: true
summary: 这是你自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要
tags:
- Hexo
- Github
- 博客
categories:
- 软件安装与配置
---
```



***相關鏈接***

- [Hexo+Github: 个人博客网站搭建完全教程(看这篇就够了)](https://www.cnblogs.com/shwee/p/11421156.html)
- [使用hexo创建github博客](http://oyjt.github.io/2016/01/14/%E4%BD%BF%E7%94%A8hexo%E5%88%9B%E5%BB%BAgithub%E5%8D%9A%E5%AE%A2/)
- [hexo超完整的搭建教程，让你拥有一个专属个人博客](https://zhuanlan.zhihu.com/p/44213627)
- [hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)