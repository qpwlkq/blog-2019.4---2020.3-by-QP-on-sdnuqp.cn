---
layout: post
title: [专题一：简单搜索]POJ-3278-Catch That Cow-BFS
date: 2019-05-19
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <queue>
    //#include <bits/stdc++.h>
    using namespace std;

    int n,k;
    bool vis[100010];
    struct p{
        int sum ;
        int x;
    };
    queue<p>q;

    bool check(p pp){
        if(pp.x >= 0 && pp.x <= 100000 && vis[pp.x] == 0){
            return 1;
        }
        else{
            return 0;
        }
    }

    void bfs(){
        while(!q.empty()){
            p pp = q.front();
            q.pop();
            p pz;

            if(pp.x == k){
                printf("%d\n",pp.sum);
                return;
            }

            pz.x = pp.x * 2;
            pz.sum = pp.sum + 1;
            if(check(pz) == 1){
                vis[pz.x] = 1;
                q.push(pz);
            }

            pz.x = pp.x + 1;
            pz.sum = pp.sum + 1;
            if(check(pz) == 1){
                vis[pz.x] = 1;
                q.push(pz);
            }

            pz.x = pp.x - 1;
            pz.sum = pp.sum + 1;
            if(check(pz) == 1){
                vis[pz.x] = 1;
                q.push(pz);
            }
        }
        return ;
    }

    int main(){
        scanf("%d %d",&n,&k);

        p pp;
        pp.x = n;
        pp.sum = 0;
        q.push(pp);
        bfs();

        return 0;
    }

<!-- /wp:code -->