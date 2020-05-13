---
layout: post
title: Codefroces-906-D-欧拉降幂
date: 2019-09-03
tags: ["数论___欧拉函数&amp;定理"]
---

<!-- wp:paragraph -->

裸(水)题,虽然刚开始我也不会.......

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

2019ICPC区域赛南京站网络赛有一个类似的题,只不过那个题要通过给你的函数看出要求什么,虽然很复杂的一个函数和描述,但是能发现答案是其实是幂塔函数取模,就是a^a^a^a^a........mod m .

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题是要求 a[1] ^ a[2] ^ a[3] ^ a[4] ^ a[5] ^ ....... .

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这两个题降幂部分是一样的 , 但是求欧拉函数的方式却不一样, 所以两个题都值得去当成模板 . 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

此题欧拉函数要通过O(根号(n))的算法求出 , 因为这个题mod的最大值是1e9.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

只能实时计算mod,而无法打表存下来,但是每次都计算会TLE在23个样例上,所以要用map随时存下来,这样可以省去很多时间.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

那个题mod的最大值是1e6 ,可以通过素数表的方式打出表.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code :

<!-- /wp:paragraph -->

<!-- wp:code -->

    #pragma warning (disable : 4996)

    #include <cstdio>
    #include <map>
    using namespace std;
    #define rep(i,a,b) for(int i = a ; i <= b ; ++i)
    const int maxn = 1e5 + 10;
    using ll = long long;

    map<ll, ll > mp;
    int a[maxn], p[maxn];

    ll phi(int n) {
        if (mp.count(n) == 1)
            return mp[n];
        ll ans = n;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                ans -= ans / i;
                while (n % i == 0)
                    n /= i;
            }
        }
        if (n > 1) ans -= ans / n;
        return mp[n] = ans;
    }

    ll mod(ll x, ll m) {
        return x < m ? x : x % m + m;
    }

    ll power(ll a, ll b, ll m) {
        ll ans = 1;
        while (b) {
            if (b & 1)
                ans = mod(ans * a, m);
            a = mod(a * a, m);
            b >>= 1;
        }
        return ans;
    }

    ll dfs(ll l, ll r, ll m) {
        if (m == 1)
            return 1;
        if (l == r)
            return a[l];
        ll res = dfs(l + 1, r , phi(m));
        return power(a[l] , res , m);
    }

    int main() {
        int n;
        ll l, r, m;
        scanf("%d %lld", &n, &m);
        rep(i, 1, n) {
            scanf("%d", &a[i]);
        }
        int t;
        scanf("%d", &t);
        rep(i, 1, t) {
            scanf("%lld %lld", &l, &r);
            ll x = dfs(l, r, m) % m ;
            printf("%d\n",x);
        }
        return 0;
    }

<!-- /wp:code -->