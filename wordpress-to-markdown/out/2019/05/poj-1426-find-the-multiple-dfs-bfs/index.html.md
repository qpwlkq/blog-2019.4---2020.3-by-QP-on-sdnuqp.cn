---
layout: post
title: [专题一：简单搜索]POJ-1426-Find The Multiple-DFS/BFS
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    /// 1

    #include <bits/stdc++.h>
    using namespace std;

    const int M = (int)1e2;

    bool flag;
    int ans[M + 5];

    void dfs(int pos, int k, int n) {
        if(flag '' pos > M)
            return;
        if(!k) {
            flag = 1;
            ans[pos] = -1;
            return;
        }
        ans[pos] = 0;
        dfs(pos + 1, (k * 10) % n, n);
        if(flag '' pos > M)
            return;
        ans[pos] = 1;
        dfs(pos + 1, (k * 10 + 1) % n, n);
        if(flag '' pos > M)
            return;
    }

    int main() {
        int n;
        while(~scanf("%d",&n) && n) {
            memset(ans,  0, sizeof(ans));
            flag = 0;
            ans[1] = 1;
            dfs(2, 1 % n, n);
            for(int i = 1; ~ans[i]; ++i)
                printf("%d", ans[i]);
            printf("\n");
        }
        return 0;
    }

    /// 2

    #include<iostream>
    #include<stdio.h>
    #include<queue>
    using namespace std;
    void bfs(int n)
    {
        queue<long long>q;
        q.push(1);
        while(!q.empty())
        {
            int i;
            long long x;
            x=q.front();
            q.pop();
            if(x%n==0)
            {
                printf("%lld\n",x);
                return ;
            }
            q.push(x*10);
            q.push(x*10+1);
        }
    }
    int main()
    {
        int n;
        while(scanf("%d",&n)&&n)
        {
            bfs(n);
        }
        return 0;
    }

<!-- /wp:code -->