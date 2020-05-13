---
layout: post
title: UVA-12716-GCD XOR
date: 2019-08-12
tags: ["数论___GCD/EXGCD"]
---

<!-- wp:paragraph -->

紫薯p318上的例题

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

并没有看懂刘大爷再说什么。。。n(log(n)^2) 的算法也不知道怎么实现的。。。怎么就logn了呢。。ORZ。。。请看下面这位同学的blog。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[传送门](https://blog.csdn.net/shimmer_/article/details/38492143)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

不过这个题最重要的地方应该是c = a - b吧，刘大爷直接明确说了，但自己不一定能推出来吧，我大概会暴力的去gcd

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

学到了，倍增的话可以将所有情况遍历一遍，并且时间复杂度还比较低(这个题打表时的确运行要明显卡顿一下，n <= 3e7)

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    #define ll long long
    typedef unsigned long long ull;
    #define maxn 30000000
    #define INF 1<<30

    int s[30000000 + 10];

    void init() {
        int sum = 0;
        for (int c = 1; c <= maxn / 2; c++) {
            for (int a = c + c; a <= maxn; a += c) {
                int b = a - c;
                if ((a ^ b) == c)
                    s[a]++;
            }
        }
        for (int i = 2; i <= maxn; i++)
            s[i] += s[i - 1];
    }

    int main() {
        int counts = 0, num;
        scanf("%d", &num);
        init();
        while (num--) {
            int n;
            scanf("%d", &n);
            printf("Case %d: %d\n", ++counts, s[n]);
        }
        return 0;
    }

<!-- /wp:code -->