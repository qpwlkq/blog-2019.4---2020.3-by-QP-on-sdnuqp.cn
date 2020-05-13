---
layout: post
title: EXGCD拓展欧几里得算法
date: 2019-08-12
tags: ["数论___GCD/EXGCD"]
---

<!-- wp:paragraph -->

很精妙的算法，通过简单的递归，就能够求出一组解，满足ax+by = GCD(a,b);

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个等式是一个贝祖等式，贝祖定理(裴蜀定理)详见：[传送门](https://baike.baidu.com/item/裴蜀定理/5186593?fr=aladdin&fromtitle=%E8%B4%9D%E7%A5%96%E5%AE%9A%E7%90%86&fromid=5185441 "%E8%B4%9D%E7%A5%96%E5%AE%9A%E7%90%86&fromid=5185441")

<!-- /wp:paragraph -->

<!-- wp:code -->

    Code 1:

    #include <bits/stdc++.h>
    using namespace std;
    int a, b, x, y；

    void EXGCD(int a, int b, int &x, int &y) {
        if (!b) { x = 1; y = 0; return; }
        EXGCD(b, a%b, y, x);
        y -= a / b * x;
    }

    int main() {
        scanf("%d %d", &a, &b);
        EXGCD(a,b,x,y);
        printf("%d %d", x, y);
        return 0;
    }

<!-- /wp:code -->

<!-- wp:code -->

    Code 2:

    #include <bits/stdc++.h>
    using namespace std;
    #define pir pair<int,int>    
    int a, b, x, y;

    pir EXGCD(int a,int b) {
        if (!b) return make_pair(1, 0);
        pir tmp = EXGCD(b, a%b);
        return make_pair(tmp.second ,tmp.first - a/b*tmp.second);
    }

    int main() {
        scanf("%d %d", &a, &b);
        pir ans = EXGCD(a,b);
        printf("%d %d",ans.first,ans.second);
        return 0;
    }

<!-- /wp:code -->