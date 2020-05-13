---
layout: post
title: using的用法
date: 2019-06-10
tags: ["基础__C++11"]
---

<!-- wp:paragraph -->

我们知道常规用法（大部分人也只会这种用法。。。）: 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

使用名称空间。

<!-- /wp:paragraph -->

<!-- wp:code -->

    using namespace std;

<!-- /wp:code -->

<!-- wp:paragraph -->

第二种用法：

<!-- /wp:paragraph -->

<!-- wp:code -->

    using ll = long long ;

<!-- /wp:code -->

<!-- wp:paragraph -->

没见过的，第一眼肯定很惊讶，心中想："卧槽，什么鬼东西？心中万匹草泥马跑过。。。。"

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

但是一运行，没报错！？这是转念一想："估计又是C11里的神奇东东"

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

百度一下，发现果然是C++11中的特殊用法

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

它等于：

<!-- /wp:paragraph -->

<!-- wp:code -->

    typedef long long ll;

<!-- /wp:code -->

<!-- wp:paragraph -->

作用叫：设置别名

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个作用，我只是举了最简单的一个例子，更高级的请自行百度。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

各种神奇的起别名。。。。。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

第三种是在子类中引用基类成员

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

类我还没怎么学，以后再说了。

<!-- /wp:paragraph -->