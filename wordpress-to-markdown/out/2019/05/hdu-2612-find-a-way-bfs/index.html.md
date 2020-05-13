---
layout: post
title: [专题一：简单搜索]HDU-2612-Find a way-BFS
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int n,m;
    int cx,cy;
    int fx,fy;
    int c[1010][1010];
    int vis1[1010][1010];
    int vis2[1010][1010];
    int des[5][2] = {{0,0},{0,1},{0,-1},{1,0},{-1,0}};

    struct p {
        int x;
        int y;
    };

    bool check(int x,int y){
        if(x >= 1 && x <= n && y >= 1 && y <= m && (c[x][y] == '.'''c[x][y] == '@')){
            return 1 ;
        }
        return 0;
    }

    queue<p>q1;

    void bfs1(){
        while(!q1.empty()){
            p pp = q1.front();
            q1.pop();
            p pz;
            for(int i = 1; i <= 4 ; i++){
                pz.x = pp.x + des[i][0] ;
                pz.y = pp.y + des[i][1] ;
                if(check(pz.x,pz.y)){
                    if(vis1[pz.x][pz.y] == 0){
                        vis1[pz.x][pz.y] = vis1[pp.x][pp.y] + 1;
                        q1.push(pz) ;
                    }
                }
            }
        }
    }

    queue<p>q2;

    void bfs2(){
        while(!q2.empty()){
            p pp = q2.front();
            q2.pop();
            p pz;
            for(int i = 1; i <= 4 ; i++){
                pz.x = pp.x + des[i][0] ;
                pz.y = pp.y + des[i][1] ;
                if(check(pz.x,pz.y)){
                    if(vis2[pz.x][pz.y] == 0){
                        vis2[pz.x][pz.y] = vis2[pp.x][pp.y] + 1;
                        q2.push(pz) ;
                    }
                }
            }
        }
    }

    struct person {
        int x;
        int y;
        int cnt;
    };

    int main(){
        while(scanf("%d %d",&n,&m) != EOF){
            getchar();
            memset(vis1,0,sizeof vis1);
            memset(vis2,0,sizeof vis2);

            for(int i = 1; i <= n ; i++){
                for(int j = 1 ; j <= m ; j++){
                    scanf("%c",&c[i][j]);
                    if(c[i][j] == 'Y'){
                        c[i][j] = '.';
                        vis1[i][j] = 1;
                        p pp;
                        pp.x = i;
                        pp.y = j;
                        q1.push(pp);
                    }
                    if(c[i][j] == 'M'){
                        c[i][j] = '.';
                        vis2[i][j] = 1;
                        p pp;
                        pp.x = i;
                        pp.y = j;
                        q2.push(pp);
                    }
                }
                getchar();
            }

            bfs1();
            bfs2();
    //        for(int i = 1; i <= n ; i++){
    //            for(int j = 1 ; j <= m ; j++){
    //                printf("%d ",vis1[i][j]);
    //            }
    //            printf("\n");
    //        }
    //        for(int i = 1; i <= n ; i++){
    //            for(int j = 1 ; j <= m ; j++){
    //                printf("%d ",vis2[i][j]);
    //            }
    //            printf("\n");
    //        }

            int maxx = 10000;
            for(int i = 1; i <= n ; i++){
                for(int j = 1; j <= m ; j++){
                    if(c[i][j] == '@' && vis1[i][j] != 0 && vis2[i][j] != 0){
                        maxx = min(maxx,vis1[i][j] + vis2[i][j] -2);
                    }
                }
            }
            printf("%d\n",maxx*11);
        }
    }

    /*

    4 4
    Y.#@
    ....
    .#..
    @..M
    4 4
    Y.#@
    ....
    .#..
    @#.M
    5 5
    Y..@.
    .#...
    .#...
    @..M.
    #...#

    */

<!-- /wp:code -->