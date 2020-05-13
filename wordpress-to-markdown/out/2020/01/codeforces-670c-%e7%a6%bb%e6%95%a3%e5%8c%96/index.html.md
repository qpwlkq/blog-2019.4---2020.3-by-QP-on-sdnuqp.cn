---
layout: post
title: Codeforces-670C-离散化
date: 2020-01-30
tags: ["基础__STL"]
---

<!-- wp:code -->

    离散化之后排序, 统计每种语言人数

    #include <bits/stdc++.h>
    using namespace std;
    const int INF = 0x3f3f3f3f;
    const int maxn = 2e6 + 10;

    int n, m;
    int a[maxn], b[maxn], c[maxn];
    int sum[maxn];
    int cnt;
    int d[maxn];
    int num[maxn];
    int ct2;

    int query(int x) {
        return lower_bound(num + 1, num + ct2 + 1, x) - num;
    }

    int main() {
        scanf("%d", &n);
        for (int i = 1; i <= n; i++) {
            scanf("%d", &a[i]);
            d[++cnt] = a[i];
        }

        scanf("%d", &m);
        for (int i = 1; i <= m; i++) {
            scanf("%d", &b[i]);
            d[++cnt] = b[i];
        }

        for (int i = 1; i <= m; i++) {
            scanf("%d", &c[i]);
            d[++cnt] = c[i];
        }

        sort(d + 1, d + cnt + 1);
        for (int i = 1; i <= cnt; i++) {
            if (i == 1 '' d[i] != d[i - 1])
                num[++ct2] = d[i];
        }

        for (int i = 1; i <= n; i++) {
            int id = query(a[i]);
            sum[id]++;
        }

        int bmax = -1, cmax = -1, ans = 0;
        for (int i = 1; i <= m; i++) {
            int x = query(b[i]);
            int y = query(c[i]);
            if (sum[x] > bmax) {
                bmax = sum[x], cmax = sum[y];
                ans = i;
            }
            else if(sum[x] == bmax){
                if (sum[y] > cmax) {
                    bmax = sum[x], cmax = sum[y];
                    ans = i;
                }
            }
        }
        printf("%d\n", ans);
        return 0;
    }

<!-- /wp:code -->