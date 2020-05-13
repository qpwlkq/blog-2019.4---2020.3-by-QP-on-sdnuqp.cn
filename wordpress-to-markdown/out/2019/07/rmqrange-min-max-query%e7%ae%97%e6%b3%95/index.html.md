---
layout: post
title: RMQ(Range Min/Max Query)算法
date: 2019-07-19
tags: ["数据结构__RMQ","算法"]
---

<!-- wp:paragraph -->

区间最值查询算法

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

采用dp的思想

<!-- /wp:paragraph -->

<!-- wp:code -->

    /*

    RMQ算法
    区间最值查询算法

    */

    #include <bits/stdc++.h>
    using namespace std;

    int n;
    int a[101];
    int dp[101][101];

    int RMQ_init() {
        for(int i = 1; i <= n; i++) {
            dp[i][0] = a[i];
        }
        for(int j = 1; (1 << j) <= n ; j++) {
            for(int i = 1; i + (1 << j) - 1 <= n; i++) {
                dp[i][j] = min(dp[i][j - 1], dp[i + (1 << j - 1)][j - 1]);
            }
        }
    }

    int RMQ_query(int l, int r) {
        int k = log2(r - l + 1);
        return min(dp[l][k], dp[r - (1 << k) + 1][k]);
    }

    int main() {
        scanf("%d", &n);
        for(int i = 1; i <= n ; i++) {
            scanf("%d", &a[i]);
        }
        RMQ_init();
        int a, b;
        while(scanf("%d %d",&a,&b) != EOF) {
            int x = RMQ_query(a, b);
            printf("%d\n", x);
        }
        return 0;
    }

    /*

    10
    1 3 7 2 5 8 9 4 10 6
    2 2
    2 3
    2 4
    5 10

    */

<!-- /wp:code -->