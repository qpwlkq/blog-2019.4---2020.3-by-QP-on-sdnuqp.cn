---
layout: post
title: 关于scanf()输入形式吃字符问题
date: 2019-06-01
tags: ["杂项"]
---

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">经常做到字符串的题，总是因为字符串读入浪费大量的时间，所以这次特别来整理一下scanf吃回车空格的问题。
 先看如下程序：
 include 
 using namespace std;
 int main(){
     int a,b;
     scanf("%d:%d",&a,&b);
     printf("%d %d\n",a,b);
     return 0;
 }
 输入:123:123回车
 输出:123 123
 输入:123:      123回车
 输出:123 123
 输入:123 :123回车
 输出:123 随机数；
 再来看如下程序：
 include 
 using namespace std;
 int main(){
     int n;
     scanf("%d\n",&n);
     printf("%d\n",n);
     return 0;
 }
 输入:123回车
 程序未结束
 继续输入空白字符（回车，空格，制表符）程序未结束，输入其他字符，程序结束
 输出:123
 所以在scanf后面加个\n，能够吃掉后面连着的所有回车，而有些题输入第一行是空格，并且多组输入，所以就不对了，被坑惨了，555；
 以后吃一个回车，老实用getchar()就好了。</pre>
<!-- /wp:preformatted -->