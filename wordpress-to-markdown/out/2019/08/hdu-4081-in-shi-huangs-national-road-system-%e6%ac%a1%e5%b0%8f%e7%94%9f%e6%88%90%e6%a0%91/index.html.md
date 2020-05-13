---
layout: post
title: HDU-4081-in Shi Huang's National Road System-次小生成树
date: 2019-08-12
tags: ["图论__次小生成树"]
---

<!-- wp:code -->

    /*
    次小生成树
    */

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int maxn = 1e3 + 10;
    const int INF = 0x3f3f3f3f;
    #define rep(i,a,b) for(int i=a ; i<=b ; ++i)

    double mp[maxn][maxn];
    double lowcost[maxn];
    double maxx[maxn][maxn];
    double xy[maxn][2];
    double a[maxn];
    bool used[maxn][maxn];
    bool vis[maxn];
    int pre[maxn];

    inline double getdis(double x1, double y1, double x2, double y2) {
        return sqrt((x1 - x2) * (x1 - x2) + (y1 - y2) * (y1 - y2));
    }

    double prim(int n) {
        memset(vis, 0, sizeof vis);
        memset(used, 0, sizeof used);
        memset(maxx, 0, sizeof maxx);
        rep(i, 1, n) {
            lowcost[i] = mp[1][i];
            pre[i] = 1;
        }
        vis[1] = 1;
        double res = 0;
        int idx;
        rep(i, 2, n) {
            idx = -1;
            rep(j, 2, n) if (!vis[j]) {
                if (idx == -1 '' lowcost[idx] > lowcost[j]) {
                    idx = j;
                }
            }
            if (idx == -1)
                return res;
            res += lowcost[idx];
            vis[idx] = 1;
            used[idx][pre[idx]] = used[pre[idx]][idx] = true;
            rep(j, 1, n) {
                if (vis[j] && j != idx) {
                    maxx[idx][j] = maxx[j][idx] = max(maxx[j][pre[idx]], lowcost[idx]);
                }
                if (!vis[j] && lowcost[j] > mp[idx][j]) {
                    lowcost[j] = mp[idx][j];
                    pre[j] = idx;
                }
            }
        }
        return res;
    }

    int main() {
        int T;
        int n;
        scanf("%d", &T);
        while (T--) {
            memset(mp, 0, sizeof mp);
            scanf("%d", &n);
            rep(i, 1, n) {
                scanf("%lf %lf %lf", &xy[i][0], &xy[i][1], &a[i]);
            }
            rep(i, 1, n) {
                rep(j, 1, n) if (i != j) {
                    mp[i][j] = getdis(xy[i][0], xy[i][1], xy[j][0], xy[j][1]);
                }
            }
            double len = prim(n);
            //printf("%f\n",len);
            double ans = -1;
            rep(i, 1, n) {
                rep(j, 1, n) if (i != j) {
                    if (used[i][j]) {
                        ans = max(ans, (a[i] + a[j]) / (len - mp[i][j]));
                    }
                    else {
                        ans = max(ans, (a[i] + a[j]) / (len - maxx[i][j]));
                    }
                }
            }
            printf("%.2f\n", ans);
        }
        return 0;
    }

<!-- /wp:code -->