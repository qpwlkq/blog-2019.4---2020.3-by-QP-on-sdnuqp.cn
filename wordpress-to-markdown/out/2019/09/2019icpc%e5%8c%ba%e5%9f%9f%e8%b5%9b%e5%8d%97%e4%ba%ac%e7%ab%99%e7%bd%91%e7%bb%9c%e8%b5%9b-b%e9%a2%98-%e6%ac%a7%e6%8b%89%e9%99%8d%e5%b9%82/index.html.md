---
layout: post
title: 2019ICPC区域赛南京站网络赛 - B题 - 欧拉降幂
date: 2019-09-03
tags: ["数论___欧拉函数&amp;定理"]
---

<!-- wp:paragraph -->

首先要通过给你的"诡异"的公式看出 , 实际上要求幂塔函数 a^a^a^a (b个) mod m.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

实际上是个裸题,可惜我不会.....排名从106 一直掉到500多....

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这里欧拉函数是用素数筛的方式提前打表,关于欧拉函数,会单独写篇博客.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

对比另一道题. codefroces 906 D

<!-- /wp:paragraph -->

<!-- wp:code -->

    #pragma warning(disable : 4996)

    #include <bits/stdc++.h>
    using namespace std;
    using ll = long long;
    const int maxn = 1e6 + 10;

    int m[maxn], phi[maxn], p[maxn], nump;

    void get_prime() {
        phi[1] = 1;
        for (int i = 2; i <= maxn; ++i) {
            if (!m[i]) {
                p[++nump] = i;
                phi[i] = i - 1;
            }
            for (int j = 1; j <= nump && p[j] * i <= maxn; ++j) {
                m[p[j] * i] = 1;
                if (i % p[j] == 0) {
                    phi[p[j] * i] = phi[i] * p[j];
                    break;
                }
                else
                    phi[p[j] * i] = phi[i] * (p[j] - 1);
            }
        }
    }

    ll mod(ll x, ll m) {
        return x < m ? x : x % m + m;
    }

    ll power(ll a, ll b, ll m) {
        ll ans = 1;
        while (b) {
            if (b & 1)
                ans = mod(ans*a , m);
            a = mod(a * a, m);
            b >>= 1;
        }
        return ans;
    }

    ll dfs(int a ,int b ,int m) {
        if (b == 0)
            return 1;
        if (m == 1)
            return a;
        ll res = dfs(a, b - 1, phi[m]);
        return power(a, res, m);
    }

    int main() {
        get_prime();
        int T;
        ll a, b, m;
        scanf("%d",&T);
        while(T--) {
            scanf("%lld %lld %lld",&a,&b,&m);
            ll x = dfs(a,b,m) % m;
            printf("%lld\n",x);
        }
        return 0;
    }

    /*

    5
    2 0 3
    3 1 2
    3 1 100
    3 2 16
    5 3 233

    */

<!-- /wp:code -->