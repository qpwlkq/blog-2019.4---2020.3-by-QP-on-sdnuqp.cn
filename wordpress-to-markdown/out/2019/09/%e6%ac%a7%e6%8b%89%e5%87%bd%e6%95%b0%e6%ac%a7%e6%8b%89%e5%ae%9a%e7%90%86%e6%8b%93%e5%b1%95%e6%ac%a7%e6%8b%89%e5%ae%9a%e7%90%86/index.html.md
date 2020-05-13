---
layout: post
title: 欧拉函数,欧拉定理,拓展欧拉定理
date: 2019-09-03
tags: ["数论___欧拉函数&amp;定理","欧拉函数","欧拉定理"]
---

<!-- wp:code -->

    1.欧拉函数
    2.欧拉定理
    3.拓展欧拉定理
    4.欧拉降幂

    1.欧拉函数
    Φ(n) = 小于等于n的与n互质的数的数量 (Φ(1) = 1)
    计算公式:Φ(n) = ∏(p - 1)p^(a[p] - 1) = n∏(1 - 1/p);
    if(n&1) Φ(n) = n-1;
    if(n&1 && b mod a == 0) Φ(a*b) = Φ(b) * a;
    if(gcd(a,b) == 1) Φ(a*b) = Φ(a) * Φ(b);
    编程实现:

    方法1 素数表法:

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 1e5;

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

    int main() {
        get_prime();
        for (int i = 1; i <= 10; i++)
            printf("%d ",phi[i]);
        return 0;
    }

    方法2 根号(n) 暴力:

    ll Euler(int n) {
        ll ans = n;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                ans -= ans / i;
                while (n % i == 0)
                    n /= i;
            }
        }
        if (n > 1) ans -= ans / n;
        return ans;
    }
    方法3 递推 :

    #pragma warning (disable : 4996)

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 1e5;
    #define rep(i,a,b) for(int i = a ; i <= b ; ++i)

    int phi[maxn];

    void Euler() {
        rep(i, 1, maxn)
            phi[i] = i;
        rep(i, 2, maxn)
            phi[i++] /= 2;
        rep(i, 3, maxn) {
            if (phi[i] == i) {
                rep(j, i, maxn) {
                    phi[j] -= phi[j] / i;
                    j += i - 1;
                }
            }
            i++;
        }
    }

    int main() {
        Euler();
        rep(i, 1, 10)
            printf("%d ",phi[i]);
        return 0;
    }

    2.欧拉定理 

    欧拉定理 : 当a,m互质时,a^Φ(m) ≡ 1 (mod m);
    费马小定理 : 当m为质数且a不为m的倍数时,a^(m-1) ≡ 1 (mod m);

    3.拓展欧拉定理

    a^c = a^(c mod Φ(m)) , gcd(a,m) = 1;
        = a^c            , gcd(a,m) != 1 && c < Φ(m)
        = a^((c mod Φ(m)) + Φ(m)) , gcd(a,m) != 1, c >= Φ(m)

<!-- /wp:code -->