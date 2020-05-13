---
layout: post
title: 欧几里得算法gcd
date: 2019-07-26
tags: ["数论___GCD/EXGCD"]
---

<!-- wp:code -->

    //辗转相除法

    #include <bits/stdc++.h>
    using namespace std;

    int n, m;

    int gcd(int a, int b) {
        printf("%d %d\n", a, b);
        return b == 0 ? a : gcd(b, a % b);
    }

    int main(){
        scanf("%d %d", &n, &m);
        printf("%d ", gcd(n, m));
        return 0;
    }

    /*
    输入：
    10 6

    输出：
    10 6
    6 4
    4 2
    2 0
    2
    */

<!-- /wp:code -->

<!-- wp:code -->

    求证：gcd(n,m) == gcd(m,b);
    设：
    1.gcd(n,m)表示n和m的最大公约数
    2.c = gcd(n,m);
    3.n = m*a + b;
    4.d = gcd(m,b);
    证：
    ∵c = gcd(n,m)
    ∴c'n ,c'm
    ∵c'm
    ∴c'm*a
    ∵c'n
    ∴c'(m*a+b)
    ∴c'b;
    ∴c'd,c是m,b的一个约数

    ∵d = gcd(m,b)
    ∴d'm , d'b;
    ∴d'm*a
    ∴d'(m*a+b)
    ∴d'n
    又d'm
    ∴d'c,d是n,m的一个约数

    综上所述
    d'c且c'd
    故d == c
    即gcd(n,m) == gcd(m,n%m);

<!-- /wp:code -->