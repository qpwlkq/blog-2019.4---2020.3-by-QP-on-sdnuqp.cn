---
layout: post
title: POJ-1679-The Unique MST-次小生成树
date: 2019-08-12
tags: ["图论__次小生成树"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int maxn = 1e3 + 10;
    const int INF = 0x3f3f3f3f;
    #define rep(i,a,b) for(int i = (a) ; i <= (b) ; ++i)

    int res;
    int lowcost[maxn];
    int pre[maxn];
    bool vis[maxn];
    int maxx[maxn][maxn]; ////
    bool used[maxn][maxn];////
    int cost[maxn][maxn];

    void init() {
        memset(cost, INF, sizeof cost);
        memset(vis, 0, sizeof vis);
        memset(maxx, 0, sizeof maxx);
        memset(used, 0, sizeof used);
    }

    int Prim(int cost[][maxn], int n) {
        rep(i, 1, n) {
            lowcost[i] = cost[1][i];
            pre[i] = 1;
        }
        vis[1] = 1;
        lowcost[1] = 0;
        int res = 0;
        int index;
        int min_value;
        rep(i, 2, n) {
            index = -1;
            min_value = INF;
            rep(j, 2, n) {
                if (min_value > lowcost[j] && !vis[j]) {
                    min_value = lowcost[j];
                    index = j;
                }
            }
            if (min_value == INF '' index == -1)
                return res;
            vis[index] = 1;
            used[index][pre[index]] = used[pre[index]][index] = 1;
            res += min_value;
            maxx[index][pre[index]] = maxx[pre[index]][index] = min_value;
            rep(j, 1, n) { 
                if (vis[j] && j != index) {
                    maxx[j][index] = maxx[index][j] = max(maxx[j][pre[index]], lowcost[index]);
                }
                if (!vis[j] && lowcost[j] > cost[index][j]) {
                    lowcost[j] = cost[index][j];
                    pre[j] = index;
                }
            }
        }
        return res;
    }

    int main() {
        int n, m;
        int T;
        scanf("%d", &T);
        while (T--){
            init();
            scanf("%d %d", &n, &m);
            int a, b, c;
            rep(i, 1, m) {
                scanf("%d %d %d", &a, &b, &c);
                cost[a][b] = cost[b][a] = c;
            }
            int x = Prim(cost, n);
            int flag = 0;
            for (int i = 1; !flag && i <= n; i++) {
                rep(j, 1, n) {
                    if (maxx[i][j] == INF '' used[i][j] == 1)
                        continue;
                    if (maxx[i][j] == cost[i][j]) {
                        flag = 1;
                        break;
                    }
                }
            }
            if (flag) {
                printf("Not Unique!\n");
            }
            else
                printf("%d\n",x);
        }
        return 0;
    }

<!-- /wp:code -->