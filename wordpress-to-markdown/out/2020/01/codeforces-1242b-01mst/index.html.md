---
layout: post
title: CodeForces-1242B-01MST
date: 2020-01-31
tags: ["基础__STL"]
---

<!-- wp:paragraph -->

这个题题意是: 给你一张图, 有n个点, 完全图, 有m条边边权1, 其余为0. 让你去求这个图最小生成树的边

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题方法有很多, 用krusral的, dfs暴力, 贪心的都有, 可惜我都不会.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

决定看一下补图连通块个数,

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

图G的补图 : 通俗的来讲就是完全图K<sub>n</sub>去除G的边集后得到的图K<sub>n</sub>-G。在图论里面，一个图_G_的**补图**（complement）或者反面（inverse）是一个图有着跟_G_相同的点，而且这些点之间有边相连当且仅当在_G_里面他们没有边相连。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

另一个求补图连通块个数的题目 : [[Codeforces 920E]Connected Components?](https://www.cnblogs.com/NaVi-Awson/p/8682506.html)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题大佬code:

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[https://www.cnblogs.com/NaVi-Awson/p/11823608.html](https://www.cnblogs.com/NaVi-Awson/p/11823608.html)

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    #define pb push_back
    using namespace std;
    const int N = 100000+5;

    int n, m, u, v, vis[N], undo[N], ans, lst[N], nxt[N];
    vector<int> to[N];
    queue<int> Q;

    void delet(int x) {nxt[lst[x]] = nxt[x], lst[nxt[x]] = lst[x]; }
    int main() {
        scanf("%d%d", &n, &m);
        for (int i = 1; i <= m; i++)
            scanf("%d%d", &u, &v), to[u].pb(v), to[v].pb(u);
        nxt[0] = 1;
        for (int i = 1; i < n; i++) lst[i+1] = i, nxt[i] = i+1;
        for (int i = 1; i <= n; i++)
            if (!vis[i]) {
                ++ans; Q.push(i); vis[i] = 1; delet(i);
                while (!Q.empty()) {
                    int u = Q.front(); Q.pop();
                    for (auto v : to[u])
                        if (!vis[v]) undo[v] = 1;
                    for (int j = nxt[0]; j; j = nxt[j])
                        if (undo[j] == 0) Q.push(j), vis[j] = 1, delet(j);
                        else undo[j] = 0;
                }
            }
        printf("%d\n", ans-1);
        return 0;   
    }

<!-- /wp:code -->