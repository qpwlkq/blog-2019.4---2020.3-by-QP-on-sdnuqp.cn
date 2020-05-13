---
layout: post
title: CodeForces-705C- 思维+模拟
date: 2020-01-30
tags: ["基础__STL"]
---

<!-- wp:paragraph -->

只会暴力肯定无限超时, 要记录每一个的x值前面的第一个x值的位置. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

大佬的题解 : [https://blog.csdn.net/codeblocksm/article/details/52230380](https://blog.csdn.net/codeblocksm/article/details/52230380)

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    const int N = 3 * 1e5 + 100;
    int arr[N], tail[N], pre[N], vis[N];

    int main()
    {
        int n, q, id = 0, sum = 0, last = 0;
        scanf("%d%d", &n, &q);
        memset(tail, -1, sizeof(tail));
        memset(pre, -1, sizeof(pre));

        while (q--) {
            int op, x;
            scanf("%d%d", &op, &x);
            if (op == 1) {
                pre[++id] = tail[x];
                tail[x] = id;
                sum++;
            }
            else if (op == 2{
                int tmp = tail[x];
                    while (tmp != -1 && !vis[tmp]) {
                        vis[tmp] = true;
                            tmp = pre[tmp];
                            sum--;
                    }
            }
            else {
                for (int i = last + 1; i <= x; i++) {
                    if (!vis[i]) {
                        sum--;
                        vis[i] = true;
                    }
                }
                last = max(last, x);
            }
            printf("%d\n", sum);
        }
        return 0;
    }

<!-- /wp:code -->