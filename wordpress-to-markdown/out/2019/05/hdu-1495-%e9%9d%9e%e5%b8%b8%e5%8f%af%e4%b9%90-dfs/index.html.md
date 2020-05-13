---
layout: post
title: [专题一：简单搜索]HDU-1495-非常可乐-DFS
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    //交C++200ms，交G++TLE;
    //#pragma GCC optimize(2)

    #include <cstdio>
    #include <iostream>
    #include <algorithm>
    #include <cstring>
    #include <queue>
    using namespace std;

    int a,b,c;
    int vis[110][110][110];
    struct p {
        int L1;
        int L2;
        int L3;
        int cnt;
    };

    queue<p>q;

    void bfs() {
        p p1;
        p1.cnt = 0;
        p1.L1 = a;
        p1.L2 = 0;
        p1.L3 = 0;
        q.push(p1);
        vis[a][0][0] = 1;
        while(!q.empty()) {
            p pp = q.front();
            q.pop();
            if((pp.L1 == a/2 && pp.L2 == a/2) '' (pp.L1 == a/2 && pp.L3 == a/2) '' (pp.L2 == a/2 && pp.L3 == a/2)) {
                printf("%d\n",pp.cnt);
                while(!q.empty()){
                    q.pop();
                }
                return ;
            }
            p pz;
            pz.cnt = pp.cnt + 1;

            if(b - pp.L2 >= pp.L1) {
                pz.L1 = 0;
                pz.L2 = pp.L2 + pp.L1;
            } else {
                pz.L1 = pp.L1 - (b - pp.L2);
                pz.L2 = b;
            }
            pz.L3 = pp.L3;
            if(vis[pz.L1][pz.L2][pz.L3] == 0) {  /// 1 -> 2
                q.push(pz);
                vis[pz.L1][pz.L2][pz.L3] = 1;
            }

            if(c - pp.L3 >= pp.L1) {
                pz.L1 = 0;
                pz.L3 = pp.L3 + pp.L1;
            } else {
                pz.L1 = pp.L1 - (c - pp.L3);
                pz.L3 = c;
            }
            pz.L2 = pp.L2;
            if(vis[pz.L1][pz.L2][pz.L3] == 0) {  /// 1 -> 3
                q.push(pz);
                vis[pz.L1][pz.L2][pz.L3] = 1;
            }

            if(a - pp.L1 >= pp.L2) {
                pz.L1 = pp.L1 + pp.L2;
                pz.L2 = 0;
            } else {
                pz.L1 = a;
                pz.L2 = pp.L2 - (a - pp.L1);
            }
            pz.L3 = pp.L3;
            if(vis[pz.L1][pz.L2][pz.L3] == 0) {  /// 2 -> 1
                q.push(pz);
                vis[pz.L1][pz.L2][pz.L3] = 1;
            }

            if(c - pp.L3 >= pp.L2) {
                pz.L2 = 0;
                pz.L3 = pp.L3 + pp.L2;
            } else {
                pz.L2 = pp.L2 - (c - pp.L3);
                pz.L3 = c;
            }
            pz.L1 = pp.L1;
            if(vis[pz.L1][pz.L2][pz.L3] == 0) {  /// 2 -> 3
                q.push(pz);
                vis[pz.L1][pz.L2][pz.L3] = 1;
            }

            if(a - pp.L1 >= pp.L3) {/////
                pz.L1 = pp.L1 + pp.L3;
                pz.L3 = 0;
            } else {
                pz.L1 = a;
                pz.L3 = pp.L3 - (a - pp.L1);
            }
            pz.L2 = pp.L2;
            if(vis[pz.L1][pz.L2][pz.L3] == 0) {  /// 3 -> 1
                q.push(pz);
                vis[pz.L1][pz.L2][pz.L3] = 1;
            }

            if(b - pp.L2 >= pp.L3) {
                pz.L2 = pp.L2 + pp.L3;
                pz.L3 = 0;
            } else {
                pz.L2 = b;
                pz.L3 = pp.L3 - (b - pp.L2);
            }
            pz.L1 = pp.L1;
            if(vis[pz.L1][pz.L2][pz.L3] == 0) {  /// 3 -> 2
                q.push(pz);
                vis[pz.L1][pz.L2][pz.L3] = 1;
            }
        }
        printf("NO\n");
    }

    int main() {
        while(scanf("%d %d %d",&a,&b,&c)!=EOF && (a&&b&&c)) {
            memset(vis,0,sizeof vis);
            if(a % 2 == 1) {
                printf("NO\n");
                continue;
            }
            bfs();
        }
        return 0;
    }

<!-- /wp:code -->