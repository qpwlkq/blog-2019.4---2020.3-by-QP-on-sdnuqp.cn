---
layout: post
title: 位运算操作
date: 2019-07-19
tags: ["杂项"]
---

<!-- wp:paragraph -->

一点小测试，后面才是正文

<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->

# include 

<!-- /wp:heading -->

<!-- wp:paragraph -->

using namespace std;

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

int lowbit(int x){  

    return x & -x;  

}

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

int main() {  

    int n;

<!-- /wp:paragraph -->

<!-- wp:code -->

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

<!-- /wp:code -->

<!-- wp:paragraph -->

}

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

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

<!-- /wp:paragraph -->