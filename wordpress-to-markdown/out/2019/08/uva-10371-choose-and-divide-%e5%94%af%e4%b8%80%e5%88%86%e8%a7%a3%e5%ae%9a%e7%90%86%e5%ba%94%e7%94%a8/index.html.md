---
layout: post
title: UVA-10371-Choose and divide-唯一分解定理应用
date: 2019-08-12
tags: ["数论___唯一分解定理"]
---

<!-- wp:paragraph -->

唯一分解定理的简单应用。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

素数要先筛出来（埃氏筛/线性筛）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

然后将因子存入数组中

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

再用公式逐项处理即可：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

C(m,n) = m! / (n! (m-n)! )

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int primes[10010];
    bool vis[10010];
    int e[10010];
    int cnt;

    void get_primes() {
        for (int i = 2; i <= 10000; i++) {
            if (vis[i] == 0) {
                primes[cnt++] = i;
                for (int j = i * i; j <= 10000; j += i) {
                    vis[j] = 1;
                }
            }
        }
    }

    void add_integer(int n,int d) {
        for (int i = 0; i < cnt ; i++) {
            while (n % primes[i] == 0) {
                n /= primes[i];
                e[i] += d;
            }
            if (n == 1)
                break;
        }
    }

    void add_factorical(int n, int d) {
        for (int i = 1; i <= n; i++) {
            add_integer(i, d);
        }
    }

    int main() {
        int p, q, r, s;
        get_primes();
        while (cin >> p >> q >> r >> s) {
            memset(e,0,sizeof e);
            add_factorical(p,1);
            add_factorical(q,-1);
            add_factorical(p-q,-1);
            add_factorical(r, -1);
            add_factorical(s, 1);
            add_factorical(r - s, 1);
            double ans = 1;
            for (int i = 0; i < cnt; i++) {
                ans *= pow(primes[i], e[i]);
            }
            printf("%.5f\n",ans);
        }
    }

<!-- /wp:code -->