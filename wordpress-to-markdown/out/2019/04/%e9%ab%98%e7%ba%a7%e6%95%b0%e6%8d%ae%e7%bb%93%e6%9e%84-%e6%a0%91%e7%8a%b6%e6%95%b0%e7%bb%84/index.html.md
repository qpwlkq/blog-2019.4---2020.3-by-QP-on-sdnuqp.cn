---
layout: post
title: 高级数据结构——树状数组
date: 2019-04-10
tags: ["数据结构__树状数组"]
---

<!-- wp:paragraph -->

膜拜bin巨  

第二篇 树状数组

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

1 - 基础，获得树状数组的值  

与线段树很像，各有优点，它编程的复杂度低于线段树，并且比线段树节省空间，但是它的使用范围较小。  

也就是说，用树状数组看可以做的题，用线段树一定可以做，而用线段树做得题，用树状数组不一定能做。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

（学习之前建议先学一下前缀和，很简单的东西，不多说。）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

树状数组可比线段树简单多了，一个是XX数组，另一个是XX树，本质不一样。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

学习博客：https://blog.csdn.net/Small_Orange_glory/article/details/81290634  

首先看树状数组中的元素，c[]是树状数组，a[]是原数组。  

c[1] = a[1];  

c[2] = a[1] + a[2];  

c[3] = a[3];  

c[4] = a[1] + a[2] + a[3] + a[4];  

c[5] = a[5];  

c[6] = a[5] + a[6];  

c[7] = a[7];  

c[8] = a[1] + a[2] + a[3] + a[4] + a[5] + a[6] + a[7] + a[8];

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

是不是很有意思？至于为什么要这么装，规律是什么？

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

来看，先将每一个数字写成二进制形式：  

1 -> 0001  

2 -> 0010  

3 -> 0011  

4 -> 0100  

5 -> 0101  

6 -> 0110  

7 -> 0111  

8 -> 1000

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

再来看每一个二进制数 从后向前数有几个0蛋,并计算2^k(k是0蛋数)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

n    k    2^k  

1 -> 0    1  

2 -> 1    2  

3 -> 0    1  

4 -> 2    4  

5 -> 0    1  

6 -> 1    2  

7 -> 0    1  

8 -> 3    8

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这时候再看c数组，知道c[n]的值怎么来得了吧，c[n] = a[n] + ... +a[n-2^k+1];(即从a[n]往前数k-1个，共k项)  

树状数组说白了就是对二进制的应用。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

为求k(最低位的1)，写出下列函数:

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

& 与运算符，只有同为1，才为1.

<!-- /wp:paragraph -->

<!-- wp:code -->

    int lowbit(int x){
         return x&(x^(x-1));
     }

<!-- /wp:code -->

<!-- wp:paragraph -->

利用补码特性也可以写成：  

<!-- /wp:paragraph -->

<!-- wp:code -->

     int lowbit(int x){
         return x&-x;
     }

<!-- /wp:code -->

<!-- wp:paragraph -->

2 - 单点更新

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

1 -> 001 c[1] += a[1];

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

lowbit(1) == 001  

1 + 001 == 010 -> 2 c[2] += a[1];

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

lowbit(2) == 010  

2 + 010 == 100 -> 4 c[4] += a[1];

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

lowbit(4) == 100  

4 + 100 == 1000-> 8 c[8] += a[1];

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

写出下列函数：

<!-- /wp:paragraph -->

<!-- wp:code -->

    void updata(int x,int y,int n){
         for(int i = x ; i <= n ; i += lowbit(i)){
             c[i] += y;
         }
     }

<!-- /wp:code -->

<!-- wp:paragraph -->

3 - 区间查询

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

区间查询是的单点更新的逆过程。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

先给出例子：

<!-- /wp:paragraph -->

<!-- wp:code -->

     num[7] = a[1] + a[2] + a[3] + a[4] + a[5] + a[6] + a[7];
     num[7] = c[4] + c[6] + c[7];
     num[111] = c[100] + c[110] + c[111];

<!-- /wp:code -->

<!-- wp:paragraph -->

上面三个式子等价。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

观察最后一个式子，简单来说，num[n] = n的二进制逐位去1，依然需要用到lowbit函数

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

通过树状数组求区间和的时间复杂度明显降低，原来可是从a[1]加到a[7]，现在只有四项相加!

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

写出下列函数：

<!-- /wp:paragraph -->

<!-- wp:code -->

    int GetSum(){
         int ans = 0;
         for(int i = x ; i > 0 ; i -= lowbit(i)){
             ans += c[i];
         }
         return ans;
     }

<!-- /wp:code -->