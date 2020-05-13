---
layout: post
title: 连通块个数-DFS/并查集
date: 2020-01-31
tags: ["基础__STL"]
---

<!-- wp:paragraph -->

DFS板子:

<!-- /wp:paragraph -->

<!-- wp:code -->

    //图的DFS遍历 计算连通块数 
    #include <iostream>
    #include <cstdio>
    #include <vector>
    #include <cstring> 
    using namespace std;
    const int nmax = 1e5 + 10;
    vector<int> G[nmax];
    int vis[nmax];//1已被访问 0未被访问 
    //遍历连通块 

    void DFS(int u) {
        vis[u] = true;
        for (int i = 0; i < G[u].size(); i++) {
            int v = G[u][i];
            if (vis[v] == 0) {//如果该节点未被访问，则深度遍历 
                DFS(v);
            }
        }
    }

    int main(int argc, char** argv) {
        int n;//点数 
        int m;//边数
        while (cin >> n >> m) {
            memset(vis, 0, sizeof(vis));
            int u, v;
            for (int i = 0; i < m; i++) {
                cin >> u >> v;
                G[u].push_back(v);
                G[v].push_back(u);
            }
            int blk = 0;
            //遍历整个图G
            for (int i = 1; i <= n; i++) {
                if (vis[i] == 0) {
                    DFS(i);//访问i所在的连通块 
                    blk++;
                }
            }
            cout << blk << endl;
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

并查集板子:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int nmax = 1010;

    int father[nmax];
    int isRoot[nmax];
    int findFather(int u) {
        if (u == father[u]) return u;//u==father[u] √;u==findFtaher[u] x 
        else {
            int f = findFather(father[u]);
            father[u] = f;
            return f;
        }
    }

    void Union(int u, int v) {
        int fu = findFather(u);
        int fv = findFather(v);
        if (fu != fv) {
            father[fu] = fv;
        }
    }
    void init(int n) {
        for (int i = 1; i <= n; i++) {
            father[i] = i;
            isRoot[i] = 0;
        }
    }

    int main(int argc, char** argv) {
        int t;
        while (cin >> t) {
            int n, m;//点数，边数 
            while (t--) {
                memset(father, 0, sizeof(father));
                memset(isRoot, 0, sizeof(isRoot));
                cin >> n >> m;
                init(n);
                int u, v;
                for (int i = 0; i < m; i++) {
                    cin >> u >> v;
                    Union(u, v);
                }
                for (int i = 1; i <= n; i++) {
                    isRoot[findFather(i)]++;
                }
                int ans = 0;
                for (int i = 1; i <= n; i++) {
                    if (isRoot[i] != 0) {
                        ans++;
                    }
                }
                cout << ans << endl;
            }
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

板子来源: https://blog.csdn.net/qian2213762498/article/details/82020882

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

ORZ

<!-- /wp:paragraph -->