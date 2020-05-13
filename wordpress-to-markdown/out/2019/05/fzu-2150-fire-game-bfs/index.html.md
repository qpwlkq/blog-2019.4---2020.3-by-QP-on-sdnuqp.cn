---
layout: post
title: [专题一：简单搜索]FZU-2150-Fire Game-BFS
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    #include <queue>
    using namespace std;

    int n,m;
    int vis[20][20];
    char c[20][20];
    int des[5][2] = {{0,0},{0,1},{0,-1},{1,0},{-1,0}};

    bool find_zero() {
        int flag = 0;
        for(int i = 1;  i<= n ; i++) {
            for(int j = 1 ; j<= m ; j++) {
                if(vis[i][j] == 0 && c[i][j] == '#') {
                    return 1;
                }
            }
        }
        return 0;
    }

    struct node {
        int x;
        int y;
        int cnt ;
    };

    queue<node>q;
    int bfs(int x, int y, int xx, int yy) {
        node p;
        p.x = x;
        p.y = y;
        p.cnt = 0;
        vis[x][y] = 1;
        q.push(p);
        node p2;
        p2.x = xx;
        p2.y = yy;
        p2.cnt = 0;
        q.push(p2);
        vis[xx][yy] = 1;
        int maxx = -1;
        while(!q.empty()) {
            node p = q.front();
            q.pop();
            maxx = max(maxx,p.cnt);
            node pp;
            for(int i = 1; i <= 4 ; i++) {
                pp.x = p.x + des[i][0];
                pp.y = p.y + des[i][1];
                pp.cnt = p.cnt + 1;
                if(pp.x > n '' pp.y > m '' pp.x  <= 0 '' pp.x <= 0)
                    continue;
                if(c[pp.x][pp.y] == '#' && vis[pp.x][pp.y] == 0) {
                    vis[pp.x][pp.y] = 1;
                    q.push(pp);
                }
            }
        }
        return maxx;
    }

    int main() {
        int t;
        scanf("%d",&t);
        int maxx = 111111;
        for(int k = 1; k <= t ; k++) {
            maxx = 111111;
            scanf("%d %d",&n,&m);
            getchar();
            for(int i = 1; i <= n ; i++) {
                for(int  j = 1; j <= m ; j++) {
                    scanf("%c",&c[i][j]);
                }
                getchar();
            }
            for(int i = 1 ; i <= n ; i++) {
                for(int j = 1 ; j <= m ; j++) {
                    if(c[i][j] == '.')
                        continue;
                    for(int l = 1 ; l <= n ; l++) {
                        for(int p = 1; p <= m ; p++) {
                            if(c[l][p] == '.') {
                                continue;
                            }
                            memset(vis,0,sizeof vis);
                            int z = bfs(i,j,l,p);
                            if(find_zero()) {
                                continue;
                            }
    //                        printf("%d %d %d %d\n",i,j,l,p);
    //                        printf("%d\n",z);
                            maxx = min(maxx,z);
                        }
                    }
                }
            }
            if(maxx == 111111) {
                printf("Case %d: -1\n",k);
            } else {
                printf("Case %d: %d\n",k,maxx);
            }
        }

    }

    /*
    2
    1 5
    #####
    5 1
    #
    #
    #
    #
    #

    */

    //                        printf("%d\n",z);
    //                        for(int i = 1 ; i<= n ; i++){
    //                            for(int j = 1; j<= m ;j++){
    //                                printf("%d ",vis[i][j]);
    //                            }
    //                            printf("\n");
    //                        }

<!-- /wp:code -->