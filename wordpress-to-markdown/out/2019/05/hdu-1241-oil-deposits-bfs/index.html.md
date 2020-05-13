---
layout: post
title: [专题一：简单搜索]HDU-1241-Oil Deposits-BFS
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int n,m;
    int c[110][110];
    int vis[110][110];
    int des[9][2] = {{0,0},{1,0},{1,1},{1,-1},{-1,0},{-1,1},{-1,-1},{0,1},{0,-1}};

    struct p {
        int x;
        int y;
    };

    bool check(int x,int y) {
        if(x >= 1 && x <= n && y >= 1 && y <= m && vis[x][y] == 1)
            return 1;
        return 0;
    }

    queue<p>q;
    int bfs(int i,int j) {
        p pd;
        pd.x = i;
        pd.y = j;
        vis[pd.x][pd.y] = 0;
        q.push(pd);
        while(!q.empty()) {
            p pp;
            pp = q.front();
            q.pop();
            p pz;
            for(int i = 1; i <= 8 ; i++) {
                pz.x = pp.x + des[i][0];
                pz.y = pp.y + des[i][1];
                if(check(pz.x,pz.y)) {
                    vis[pz.x][pz.y] = 0;
                    q.push(pz);
                }
            }
        }
    }

    int main() {
        while(scanf("%d %d",&n,&m) && (n&&m)) {
            getchar();
            for(int i = 1; i <= n ; i++) {
                for(int j = 1; j <= m ; j++) {
                    scanf("%c",&c[i][j]);
                    c[i][j] == '@'?vis[i][j] = 1:vis[i][j] = 0;
                }
                getchar();
            }
    //            getchar();
            int cnt = 0;
            for(int i = 1; i <= n ; i ++) {
                for(int j = 1; j <= m ; j++) {
                    if(vis[i][j] == 1) {
                        cnt++;
                        bfs(i,j);
                    }
                }
            }
            printf("%d\n",cnt);
    //        getchar();
        }
    }

    /*
    1 1
    *
    3 5
    *@*@*
    **@**
    *@*@*
    1 8
    @@****@*
    5 5
    ****@
    *@@*@
    *@**@
    @@@*@
    @@**@
    0 0
    */

<!-- /wp:code -->