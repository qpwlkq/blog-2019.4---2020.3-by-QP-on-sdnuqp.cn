---
layout: post
title: 矩阵快速幂
date: 2019-03-29
tags: ["杂项"]
---

<!-- wp:paragraph -->

貌似很难，其实极其简单。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

核心思想仍是找递推式，通过矩阵表示递推式罢了。。。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### Fibonacci（最简单的）

<!-- /wp:heading -->

<!-- wp:code -->

    Description
    In the Fibonacci integer sequence, F0 = 0, F1 = 1, and Fn = Fn − 1 + Fn − 2 for n ≥ 2.

    Input
    a single line containing n (where 0 ≤ n ≤ 100,000,000,000)

    Output
    print Fn mod 1000000007 in a single line.

    Sample Input
    99999999999

    Sample Output
    669753982

<!-- /wp:code -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    typedef long long ll;
    const ll MOD = 1000000007;

    struct mat {
        ll a[2][2];
    };

    mat mat_mul(mat a,mat b) {
        mat res;
        memset(res.a,0,sizeof(res.a));
        for(int i=0; i<=1 ; i++) {
            for(int j = 0; j <=1; j++) {
                for(int k = 0; k<=1 ; k++) {
                    res.a[i][j] = (res.a[i][j] + a.a[i][k]*b.a[k][j])%MOD;
                }
            }
        }
        return res;
    }

    ll mat_pow(ll n){
        mat c,res;
        c.a[0][0] = 1;
        c.a[0][1] = 1;
        c.a[1][0] = 1;
        c.a[1][1] = 0;
        memset(res.a,0,sizeof(res.a));
        res.a[0][0] = 1;
        res.a[1][1] = 1;
        while(n){
            if(n&1){
                res = mat_mul(res,c);
            }
            c = mat_mul(c,c);
            n >>=1 ;
        }
        return res.a[0][1]%MOD;
    }

    int main() {
        ll n;
        scanf("%lld",&n);

        ll ans = mat_pow(n);

        printf("%lld",ans);
    }

<!-- /wp:code -->

<!-- wp:heading {"level":3} -->

### 更复杂点的F（n）= F（n-1）+F（n-2）+F（n-3）

<!-- /wp:heading -->

<!-- wp:paragraph -->

[SDNUOJ1085爬楼梯再加强版](http://www.acmicpc.sdnu.edu.cn/problem/show/1085)

<!-- /wp:paragraph -->

<!-- wp:code -->

    Description
    WZ是个蛋痛的人，总是喜欢琢磨蛋痛的事，比如他最近想知道上楼梯总共有多少种方式。已知他一步可以迈一阶、两阶或者三阶，现在给你楼梯的阶数，让你计算总共有多少种方式。

    Input
    输入有多组数据，每组数据占一行，表示楼梯的阶数。(1<=N<=100,000,000,000)

    Output
    对于每组数据，输出一行，表示上楼方式的总数 % 1000000007。

    Sample Input
    1
    2

    Sample Output
    1
    2

<!-- /wp:code -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    typedef long long ll;
    const ll MOD = 1000000007;

    struct mat {
        ll a[3][3];
    };

    mat mat_mul(mat a,mat b) {
        mat res;
        memset(res.a,0,sizeof(res.a));
        for(int i = 0; i<=2 ; i++) {
            for(int j = 0; j<=2 ; j++) {
                for(int k = 0; k<=2 ; k++) {
                    res.a[i][j] += ( a.a[i][k] * b.a[k][j])%MOD;
                }
            }
        }
        return res;
    }

    ll mat_pow(ll n) {
        mat c,res;
        memset(c.a,0,sizeof(c.a));
        memset(res.a,0,sizeof(res.a));
        c.a[0][0] = 1;
        c.a[0][1] = 1;
        c.a[0][2] = 1;
        c.a[1][0] = 1;
        c.a[2][1] = 1;
        for(int i=0; i<3 ; i++) {
            res.a[i][i] = 1;
        }
        while(n) {
            if(n&1) {
                res = mat_mul(res,c);
            }
            c = mat_mul(c,c);
            n >>= 1;
        }
        return (res.a[0][0])%MOD;
    }

    int main() {
        ll n;
        while(scanf("%lld",&n)!=EOF) {

    //    n -= 1;

            ll ans = mat_pow(n);

            printf("%lld\n",ans);

        }
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

懒得多说，代码表达。

<!-- /wp:paragraph -->