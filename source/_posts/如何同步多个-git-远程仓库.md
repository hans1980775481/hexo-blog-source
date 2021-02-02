---
title: 如何同步多个 git 远程仓库
author: xmhans
tags:
  - git
categories:
  - 转发
  - git操作
date: 2021-02-02 10:09:49
top:
summary:
img:
---
### 日常需求
以前源码是托管在 github 的, 现在想要同步托管在 gitee, 一做备份分发, 二方便国内下载使用(网速可观), 三防止被墙…

### 方式一 使用 gitee 的强制同步
之前在 github 托管了这么一个项目 mirrors-in-china, 后来国内出了 gitee, 那么想着把项目同步一份到 gitee, 方便大家查看… 正巧 gitee 提供强制同步功能, 方便操作…

![image-20210202102142510](https://cdn.jsdelivr.net/gh/hans1980775481/picture-bed/img/image-20210202102142510.png)

我还是只用维护 github 那份源码, gitee 这边没忘记的话, 手搓点击下强制同步按钮即可.

但是容易忘记, 造成两边不完全同步.

不过我这个项目本身就非常简单, 这点同步时差完全没大问题, 够用, 并且没有其他任何多余的操作.

### 方式二 手搓 push 多次
换另一个项目来说, 我之前在 github 托管了这么一个项目 GlobalScanner.Sdk, 应广大小伙伴需求, 希望把项目在国内同步一份, 方便下载/参考/使用.

那么不外乎就是配置多个远程库地址, 多次推送咯, 那么我们先来看看现有远程库的情况:

```shell
$ git remote --verbose
origin  git@github.com:taadis/GlobalScanner.Sdk.git (fetch)
origin  git@github.com:taadis/GlobalScanner.Sdk.git (push)
```

可以看到目前仅有 git@github.com:taadis/GlobalScanner.Sdk.git 这个远程库地址.

我们来加一个 gitee 的远程地址, 首先在 gitee 建好同步仓库, 然后我们在本地添加一个新的远程库地址:

```git
$ git remote add giteeorigin git@gitee.com:taadis/GlobalScanner.Sdk.git
```
添加完成后我们查看一下:

```shell
$ git remote --verbose
giteeorigin     git@gitee.com:taadis/GlobalScanner.Sdk.git (fetch)
giteeorigin     git@gitee.com:taadis/GlobalScanner.Sdk.git (push)
origin  git@github.com:taadis/GlobalScanner.Sdk.git (fetch)
origin  git@github.com:taadis/GlobalScanner.Sdk.git (push)
```
可以查看到以下2个远程库地址:

giteeorigin: 是我们新加的 gitee 的远程库地址

origin: 是我们之前在 github 的远程库地址

接下来同步:

```shell
git add .
git commit -m "add gitee"
git push -u origin master
git push -u giteeorigin master
```

有链接有真相:

github:

https://github.com/taadis/GlobalScanner.Sdk/commit/da00f0584c5a2699bb621e99a00fe15dece33d38

gitee:

https://gitee.com/taadis/GlobalScanner.Sdk/commit/da00f0584c5a2699bb621e99a00fe15dece33d38

比之前多个一次 git push 操作…其他和之前没有太大区别…没有更多的心智负担.

但是经常容易忘记…

### 方式三 最多跑一次
不想着法偷懒的 coder 不是好程序员, 秉承 "最多跑一次" 的理念, 让我们试试怎么一次 push 统统搞定.

在本地 git 仓库里找到这个文件 .git/config, 内容如下:

```shell
[core]
    repositoryformatversion = 0
    filemode = false
    bare = false
    logallrefupdates = true
    symlinks = false
    ignorecase = true
[remote "origin"]
    url = git@github.com:taadis/GlobalScanner.Sdk.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[remote "giteeorigin"]
    url = git@gitee.com:taadis/GlobalScanner.Sdk.git
    fetch = +refs/heads/*:refs/remotes/giteeorigin/*
```
改为如下:

合并2个 remote 配置

```shell
[core]
    repositoryformatversion = 0
    filemode = false
    bare = false
    logallrefupdates = true
    symlinks = false
    ignorecase = true
[remote "origin"]
    url = git@github.com:taadis/GlobalScanner.Sdk.git
    url = git@gitee.com:taadis/GlobalScanner.Sdk.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

上面这个手动配置是为了更好的说明而已, 其实可以用以下命令简化操作, 在 origin 节点下补充了一个新的远程地址.
```shell

$ git remote set-url --add origin git@gitee.com:taadis/GlobalScanner.Sdk.git
```
看看补充后的远程地址情况

```shell
git remote --verbose
origin  git@github.com:taadis/GlobalScanner.Sdk.git (fetch)
origin  git@github.com:taadis/GlobalScanner.Sdk.git (push)
origin  git@gitee.com:taadis/GlobalScanner.Sdk.git (push)
```
注意看后面的 (fetch)(push), 相信你会明白点什么.

然后我们可以继续这样使用来实现 github & gitee 的同步推送和分发:

```shell
git add .
git commit -m "github & gitee 同步推送和分发"
git push origin master
```
有链接有真相:

github:

https://github.com/taadis/GlobalScanner.Sdk/commit/6846226ff2be56ed0f58c9345bac4a0170f1880f

gitee:

https://gitee.com/taadis/GlobalScanner.Sdk/commit/6846226ff2be56ed0f58c9345bac4a0170f1880f

可以看到, 使用上和最初没有任何区别, 只是多配置了一次, 算是实现了 "最多配(跑)一次".

### 总而言之
几种方式, 各取所需咯.