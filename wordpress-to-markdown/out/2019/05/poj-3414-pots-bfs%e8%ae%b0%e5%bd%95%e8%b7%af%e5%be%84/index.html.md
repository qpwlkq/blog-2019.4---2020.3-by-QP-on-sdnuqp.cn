---
layout: post
title: [专题一：简单搜索]POJ-3414-Pots-BFS+记录路径
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <queue>
    #include <stack>
    #include <cstring>
    #include <algorithm>
    using namespace std;

    int a,b,c;
    int vis[102][102];

    struct p {
        int x;
        int y;
        int cnt;
        int pre[102];
    };

    void check(int x) {
        if(x == 11)
            printf("DROP(1)\n");
        else if(x == 12)
            printf("DROP(2)\n");
        else if(x == 21)
            printf("FILL(1)\n");
        else if(x == 22)
            printf("FILL(2)\n");
        else if(x == 32)
            printf("POUR(1,2)\n");
        else if(x == 31)
            printf("POUR(2,1)\n");
    }

    queue<p>q;

    int dfs() {
        p p1;
        p1.x = 0;
        p1.y = 0;
        p1.cnt = 0;
        q.push(p1);
        while(!q.empty()) {
            p pp = q.front();
            q.pop();
    //        printf("%d %d %d\n",pp.x,pp.y,pp.cnt);
            if(pp.x == c '' pp.y == c) {
                printf("%d\n",pp.cnt);
                for(int i = 0 ; i <= pp.cnt ; i++) {
                    check(pp.pre[i]);
                }
                while(!q.empty()){
                    q.pop();
                }
                return 1;
            }
            p pz = pp;
            pz.cnt = pp.cnt + 1;

    //        printf("<%d>\n",pz.cnt);
            ///DROP(1)
            pz.x = 0;
            pz.y = pp.y;
            pz.pre[pz.cnt] = 11;
            if(vis[pz.x][pz.y] == 0) {
                q.push(pz);
                vis[pz.x][pz.y] = 1;
            }
            ///DROP(2)
    //        pz = pp;
            pz.x = pp.x;
            pz.y = 0;
            pz.pre[pz.cnt] = 12;
            if(vis[pz.x][pz.y] == 0) {
                q.push(pz);
                vis[pz.x][pz.y] = 1;
            }

            ///FILL(1)
    //        pz = pp;
            pz.x = a;
            pz.y = pp.y;
            pz.pre[pz.cnt] = 21;
            if(vis[pz.x][pz.y] == 0) {
                q.push(pz);
                vis[pz.x][pz.y] = 1;
            }

            ///FILL(2)
    //        pz = pp;
            pz.x = pp.x;
            pz.y = b;
            pz.pre[pz.cnt] = 22;
            if(vis[pz.x][pz.y] == 0) {
                q.push(pz);
                vis[pz.x][pz.y] = 1;
            }
            ///POUR(2,1)

    //        pz = pp;
            pz.pre[pz.cnt] = 31;
            if(pp.y >= a-pp.x) {
                pz.x = a;
                pz.y = pp.y - (a-pp.x);
                if(vis[pz.x][pz.y] == 0) {
                    vis[pz.x][pz.y] = 1;
                    q.push(pz);
                }
            } else {
                pz.x = pp.x + pp.y;
                pz.y = 0;
                if(vis[pz.x][pz.y] == 0) {
                    vis[pz.x][pz.y] = 1;
                    q.push(pz);
                }
            }
            ///POUR(1,2)
    //        pz = pp;
            pz.pre[pz.cnt] = 32;
            if(pp.x >= b - pp.y) {
                pz.x = pp.x - (b - pp.y);
                pz.y = b;
                if(vis[pz.x][pz.y] == 0) {
                    vis[pz.x][pz.y] = 1;
                    q.push(pz);
                }
            } else {
                pz.x = 0;
                pz.y = pp.y + pp.x;
                if(vis[pz.x][pz.y] == 0) {
                    vis[pz.x][pz.y] = 1;
                    q.push(pz);
                }
            }
        }
        return 0;
    }

    int main() {
        scanf("%d %d %d",&a,&b,&c);
        if(dfs())
            ;
        else{
            printf("impossible\n");
        }
    }

    /*
    6
    FILL(2)
    POUR(2,1)
    DROP(1)
    POUR(2,1)
    FILL(2)
    POUR(2,1)
    */

<!-- /wp:code -->