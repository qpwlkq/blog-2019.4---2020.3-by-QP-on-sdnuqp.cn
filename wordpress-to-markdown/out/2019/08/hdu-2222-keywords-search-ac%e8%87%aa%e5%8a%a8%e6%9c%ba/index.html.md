---
layout: post
title: HDU-2222-Keywords Search-AC自动机
date: 2019-08-17
tags: ["字符串__AC自动机"]
---

<!-- wp:paragraph -->

入门级模板题,比着斌巨模板写的:

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    #include <queue>
    //#include <bits/stdc++.h>
    using namespace std;

    struct Trie {
        int next[500010][26], fail[500010], end[500010];
        int root, L;
        int newnode() {
            for (int i = 0; i <= 25; ++i)
                next[L][i] = -1;
            end[L++] = 0;
            return L - 1;
        }
        void init() {
            L = 0;
            root = newnode();
        }
        void insert(char buf[]) {
            int len = strlen(buf);
            int now = root;
            for (int i = 0; i < len; ++i) {
                if (next[now][buf[i] - 'a'] == -1)
                    next[now][buf[i] - 'a'] = newnode();
                now = next[now][buf[i] - 'a'];
            }
            end[now]++;
        }
        void build() {
            queue<int>q;
            fail[root] = root;
            for (int i = 0; i < 26; i++)
                if (next[root][i] == -1)
                    next[root][i] = root;
                else {
                    fail[next[root][i]] = root;
                    q.push(next[root][i]);
                }
            while (!q.empty()) {
                int now = q.front();
                q.pop();
                for (int i = 0; i <= 25; ++i) {
                    if (next[now][i] == -1)
                        next[now][i] = next[fail[now]][i];
                    else {
                        fail[next[now][i]] = next[fail[now]][i];
                        q.push(next[now][i]);
                    }
                }
            }
        }
        int query(char buf[]) {
            int len = strlen(buf);
            int now = root;
            int res = 0;
            for (int i = 0; i < len; ++i) {
                now = next[now][buf[i] - 'a'];
                int temp = now;
                while (temp != root) {
                    res += end[temp];
                    end[temp] = 0;
                    temp = fail[temp];
                }
            }
            return res;
        }
    };

    char buf[1000010];
    Trie ac;

    int main() {
        int T;
        int n;
        scanf("%d",&T);
        while (T--) {
        scanf("%d", &n);
        ac.init();
        for (int i = 0; i <= n - 1; ++i) {
            scanf("%s", buf);
            ac.insert(buf);
        }
        scanf("%s", buf);
        ac.build();
        printf("%d\n", ac.query(buf));
        }
        return 0;
    }

    /*
    binju模板
    */

<!-- /wp:code -->