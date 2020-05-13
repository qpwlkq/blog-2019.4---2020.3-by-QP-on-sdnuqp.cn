---
layout: post
title: lambda表达式（λ）
date: 2019-03-29
tags: ["基础__C++11"]
---

<!-- wp:paragraph -->

C++11中有很多很好使的东西

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

比如说：lambda

<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">  "Lambda 表达式"(lambda expression)是一个[匿名函数](https://baike.baidu.com/item/%E5%8C%BF%E5%90%8D%E5%87%BD%E6%95%B0/4337265)，Lambda表达式基于数学中的[λ演算](https://baike.baidu.com/item/%CE%BB%E6%BC%94%E7%AE%97)得名，直接对应于其中的lambda抽象(lambda abstraction)，是一个匿名函数，即没有函数名的函数。Lambda表达式可以表示[闭包](https://baike.baidu.com/item/%E9%97%AD%E5%8C%85/10908873)（注意和数学传统意义上的不同）。
                                                   --------百度O_o</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->

总之，它是一个可以简写一些函数的方法，很多函数比如说在结构体排序的时候:

<!-- /wp:paragraph -->

<!-- wp:code -->

    ...
    bool cmp(node a,node b){
        return a.x < b.x
    }
    或者是
    bool cmp(int &a,int &b){
        return a < b;
    }
    ...
    int main(){
        ...
        sort(a,a+10,cmp);
        ...
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

要写一个cmp函数

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

用lanbda表达式改写一下就是：

<!-- /wp:paragraph -->

<!-- wp:code -->

    sort(a, a+n, [](int a,int b){return a>b;});

<!-- /wp:code -->

<!-- wp:paragraph -->

明显简洁多了。。。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

更高级的应用请去看 [Microsoft Docs](https://docs.microsoft.com/en-us/cpp/cpp/lambda-expressions-in-cpp?view=vs-2019)。

<!-- /wp:paragraph -->