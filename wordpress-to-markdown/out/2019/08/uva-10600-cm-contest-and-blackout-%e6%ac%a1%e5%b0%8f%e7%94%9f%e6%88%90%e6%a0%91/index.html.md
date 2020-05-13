---
layout: post
title: UVA-10600-CM Contest and Blackout-次小生成树
date: 2019-08-12
tags: ["图论__次小生成树"]
---

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    #define rep(i,a,b) for(int i=(a) ; i<=(b); ++i)
    const int maxn = 1e2 + 10;
    const int INF = 0x3f3f3f3f;

    int n, m;
    int a, b, c;

    int mp[maxn][maxn];
    int maxx[maxn][maxn];
    int lowcost[maxn];
    int pre[maxn];
    bool vis[maxn];
    bool used[maxn][maxn];

    void init() {
        memset(vis, 0, sizeof vis);
        memset(used, 0, sizeof used);
        memset(maxx, 0, sizeof maxx);
        rep(i, 1, n)
            rep(j, 1, n) {
            if (i == j)
                mp[i][j] = 0;
            else
                mp[i][j] = mp[j][i] = INF;
        }
    }

    int prim() {
        rep(i, 1, n) {
            lowcost[i] = mp[1][i];
            pre[i] = 1;
        }
        vis[1] = 1;
        int res = 0;
        rep(i, 2, n) {
            int idx = -1;
            rep(j, 2, n) if (!vis[j]) {
                if (lowcost[j] < lowcost[idx] '' idx == -1) {
                    idx = j;
                }
            }
            vis[idx] = 1;
            res += lowcost[idx];
            used[idx][pre[idx]] = used[pre[idx]][idx] = true;
            rep(j, 1, n) {
                if (vis[j] && j != idx) {
                    maxx[j][idx] = maxx[idx][j] = max(maxx[pre[idx]][j], lowcost[idx]);
                }
                if (!vis[j] && lowcost[j] > mp[j][idx]) {
                    lowcost[j] = mp[j][idx];
                    pre[j] = idx;
                }
            }
        }
        return res;
    }

    int SecMST(int num) {
        int z = INF;
        rep(i, 1, n)
            rep(j, i + 1, n)
            if (!used[i][j] && mp[i][j] != INF)
                z = min(z, num - maxx[i][j] + mp[i][j]);
        return z;
    }

    int main() {
        int T;
        scanf("%d", &T);
        while (T--) {
            scanf("%d %d", &n, &m);
            init();
            for (int i = 1; i <= m; i++) {
                scanf("%d %d %d", &a, &b, &c);
                mp[a][b] = mp[b][a] = c;
            }
            int ans = prim();
            int secans = SecMST(ans);
            printf("%d %d\n", ans, secans);
        }
    }

    /*
    2
    5 8
    1 3 75
    3 4 51
    2 4 19
    3 2 95
    2 5 42
    5 4 31
    1 2 9
    3 5 66
    9 14
    1 2 4
    1 8 8
    2 8 11
    3 2 8
    8 9 7
    8 7 1
    7 9 6
    9 3 2
    3 4 7
    3 6 4
    7 6 2
    4 6 14
    4 5 9
    5 6 10

    */

<!-- /wp:code -->