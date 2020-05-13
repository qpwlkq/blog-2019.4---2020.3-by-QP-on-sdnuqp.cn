---
layout: post
title: HDU-1364-DFS/dp
date: 2020-01-31
tags: ["基础__STL"]
---

<!-- wp:paragraph -->

DFS暴力搜索每一个点就好了, dp优雅一些

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <algorithm>
    using namespace std;
    int lim;
    int mp[150][150];
    int n, m;
    int lr[100017][2];
    char ch[100017];
    int ok(int x, int y){
        if (x <= n && x >= 1 && y >= 1 && y <= m){
            if (mp[x][y] == 0)
                return 1;
        }
        return 0;
    }

    int dfs(int x, int y, int nw){
        if (!ok(x, y))
            return 0;
        if (nw == lim)
            return 1;
        if (ch[nw] == 'R'){
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x, y + i))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x, y + i))
                    break;
                if (dfs(x, y + i, nw + 1))
                    return 1;
            }
        }
        if (ch[nw] == 'L'){
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x, y - i))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x, y - i))
                    break;
                if (dfs(x, y - i, nw + 1))
                    return 1;
            }
        }
        if (ch[nw] == 'U'){
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x - i, y))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x - i, y))
                    break;
                if (dfs(x - i, y, nw + 1))
                    return 1;
            }
        }
        if (ch[nw] == 'D')
        {
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x + i, y))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x + i, y))
                    break;
                if (dfs(x + i, y, nw + 1))
                    return 1;
            }
        }
        return 0;
    }

    int main(){
        int t;
        scanf("%d", &t);
        while (t--){
            scanf("%d%d", &n, &m);
            for (int i = 1; i <= n; i++)
                for (int j = 1; j <= m; j++)
                    scanf("%d", &mp[i][j]);
            int l, r;
            lim = 0;
            char c;
            while (scanf("%d%d", &l, &r), l '' r){
                getchar();
                cin >> c;
                if (l > r)
                    swap(l, r);
                lr[lim][0] = l;
                lr[lim][1] = r;
                ch[lim++] = c;
            }
            int ans = 0;
            for (int ii = 1; ii <= n; ii++){
                for (int j = 1; j <= m; j++){
                    if (ok(ii, j) && dfs(ii, j, 0))
                        ans++;
                }
            }
            printf("%d\n", ans);
        }
        return 0;
    }

<!-- /wp:code -->