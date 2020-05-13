---
layout: post
title: 关于位运算
date: 2019-06-03
tags: ["基础__STL","杂项"]
---

<!-- wp:paragraph -->

一点小测试。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int lowbit(int x){
        return x & -x;
    }

    int main() {
        int n;

        n = 16;

        printf("n = %d",n);
        printf("二进制:");
        while(n) {
            if(n & 1)
                printf("1");
            else
                printf("0");
            n >>= 1;
        }
        printf("\n");

        n = 16;
        printf("n'1     : %d\n",n'1);///一个为1，则为1
        printf("n'(1<<3): %d\n",n'(1<<3));///特定位赋值
        printf("n'0     : %d\n",n'0);///它本身

        printf("n&1     : %d\n",n&1);///都为1，则为1
        printf("n&0     : %d\n",n&0);///0

        printf("n^1     : %d\n",n^1);///不同为1，相同为0
        printf("n^0     : %d\n",n^0);///它本身

        printf("-n      : %d\n",-n);
        printf("n&-n    : %d\n",n&(-n));///emmmmmm，不知怎么描述...lowbit数组操作

        if(-n == ~n + 1){   ///它们相等
            printf("~n+1      :%d ",~n+1);
        }

        return 0;
    }

<!-- /wp:code -->

<!-- wp:code -->

    输出：
    n = 16二进制:00001
    n'1     : 17
    n'(1<<3): 24
    n'0     : 16
    n&1     : 0
    n&0     : 0
    n^1     : 17
    n^0     : 16
    -n      : -16
    n&-n    : 16
    ~n+1      :-16

<!-- /wp:code -->

<!-- wp:paragraph -->

Bit Twidding Hacks（外国人写的文章）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

汉译为：位运算骚操作

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

传送门：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[https://graphics.stanford.edu/~seander/bithacks.html](https://graphics.stanford.edu/~seander/bithacks.html)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

<!-- /wp:paragraph -->