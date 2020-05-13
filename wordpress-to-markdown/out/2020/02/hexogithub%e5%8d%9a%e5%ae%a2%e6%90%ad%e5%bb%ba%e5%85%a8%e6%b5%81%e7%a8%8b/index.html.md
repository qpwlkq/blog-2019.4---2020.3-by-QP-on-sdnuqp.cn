---
layout: post
title: hexo+github博客搭建全流程
date: 2020-02-02
tags: ["基础__STL"]
---

<!-- wp:code -->

    第一步:
    首先需要git和node.js
    git都有吧.
    nodejs可以去官网nodejs.org下载
    (不知道为啥nodejs/ch-zn中国官网下载超级慢, 去nodjs.org/en/下载正常...无语)

    第二步:

    win+r -> cmd

    无脑输入指令:

    npm install -g cnpm -registry=https:/registry.npm.taobao.org
    npm是包管理器, 中国么, 有高墙的呢, 所以通过npm安装cnpm, 淘宝的镜像源,  会快很多.
    这一步很快

    cnpm install -g hexo
    通过cnpm安装hexo
    这一步也很快

    mkdir blog
    创建一个新的文件夹

    cd blog
    进入

    hexo init
    众所周知, init初始化的意思
    这一步可能会卡住, 我卡了三个小时, 各种重试, 结果发现断了wifi, 连上手机热点, 1min就搞定了...无语

    hexo s
    start, 启动!!!
    这时候可以去浏览器地址栏输入 localhost:4000
    如果你进去了, 看见了hallo world
    恭喜

    第三步:

    hexo n "第一篇博客"
    new, 新建文章

    hexo clean
    清空旧的

    hexo g
    generate, 生成新的

    hexo s
    启动动动动动

    去浏览器进blog看看是否有了新文章
    如果有了
    恭喜

    第四步:
    部署到服务器上

    有钱人可以买个服务器
    穷逼可以部署到github或者gitee(码云)
    此码云非彼马云

    去github建立一个新的仓库命名为: 你的用户名.github.io
    必须这样命名!

    成功建立好了
    恭喜

    第五步:

    去cmd,
    先安装一个插件

    cnpm install --save hexo-deployer-git
    安装插件

    去blog文件夹中找到: _config.yml

    记事本打开, 找到最后两行
    改成:
    deploy:
        type: git
        repo: 你的仓库地址(https://github.com/你的用户名/你的仓库名)
        branch: master

    最后:
    hexo d
    将blog推送到github上

    去github仓库中看一下, 有文件了
    恭喜

    第六步:

    更改主题:
    https://github.com/litten/hexo-theme-yilia

    好看不亏
    完事

<!-- /wp:code -->