---
layout: post
title: Xtu-1260-Determinant-高斯消元+逆元+线代
date: 2019-10-06
tags: ["数论__高斯消元"]
---

<!-- wp:paragraph -->

这是2017年湘潭大学举办的一个大学生程序设计全国邀请赛的题目.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

xtu我搜了,根本搜不到,感觉已经凉了,比我们学校还凉.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题出的非常好.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

高斯消元可以用来做两件事,一是线性方程组求解,而是求解矩阵的逆矩阵.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题用到了第二种.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

先要转化一下,将n * (n-1)的矩阵补全成n * n的矩阵,之后求新矩阵的伴随矩阵,伴随矩阵的第一行就是题目的答案啊!(伴随矩阵要用逆矩阵求出来,'A' * A^-1 = A* , 而逆矩阵要通过矩阵初等变换求出来,当然要用Gauss消元了)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码是别人的,自己懒的写了.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[大佬的博客](https://blog.csdn.net/crazy_calf/article/details/75270151)

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    typedef long long ll;
    const int maxn = 205;
    const ll mod = 1e9 + 7;
    ll a[maxn][maxn], b[maxn][maxn];

    ll inv_(ll a, ll k) {
        ll res = 1;
        while (k) {
            if (k & 1) res = res * a % mod;
            a = a * a % mod;
            k >>= 1;
        }
        return res;
    }
    void solve(int n) {
        memset(b, 0, sizeof b);
        for (int i = 1; i <= n; i++) b[i][i] = 1;
        ll det = 1;
        for (int i = 1; i <= n; i++) {
            int t;
            for (t = i; t <= n; t++) {
                if (a[t][i]) break;
            }
            if (t != i) det *= -1;
            for (int j = 1; j <= n; j++) {
                swap(a[i][j], a[t][j]);
                swap(b[i][j], b[t][j]);
            }
            det = (det * a[i][i] % mod + mod) % mod;
            ll inv = inv_(a[i][i], mod - 2); //a[i][i]的逆元
            for (int j = 1; j <= n; j++) {
                a[i][j] = inv * a[i][j] % mod;
                b[i][j] = inv * b[i][j] % mod;
            }
            for (int k = 1; k <= n; k++) {
                if (k == i) continue;
                ll tmp = a[k][i];
                for (int j = 1; j <= n; j++) {
                    a[k][j] = (a[k][j] - a[i][j] * tmp % mod + mod) % mod;
                    b[k][j] = (b[k][j] - b[i][j] * tmp % mod + mod) % mod;
                }
            }
        }
        det = (det + mod) % mod;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                b[i][j] = det * b[i][j] % mod;  //将b由逆矩阵变成伴随矩阵
            }
        }
    }
    int main(void) {
        int n;
        while (scanf("%d", &n) != EOF) {
            for (int i = 1; i <= n; i++) a[1][i] = 1;
            for (int i = 2; i <= n; i++)
                for (int j = 1; j <= n; j++)
                    scanf("%lld", &a[i][j]);
            solve(n);
            for (int i = 1; i <= n; i++)
                printf("%lld%c", (i & 1 ? b[i][1] : (mod - b[i][1]) % mod), i == n ? '\n' : ' ');
        }
        return 0;
    }

<!-- /wp:code -->