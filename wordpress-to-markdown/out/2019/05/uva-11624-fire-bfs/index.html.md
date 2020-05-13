---
layout: post
title: [专题一：简单搜索]UVA-11624-Fire!-BFS
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
    int vis[1010][1010];
    int mark[1010][1010];
    int des[5][2] = {{0,0},{0,1},{0,-1},{1,0},{-1,0}};

    struct p {
        int x;
        int y;
    };

    bool check(int x,int y){
        if(x >= 1 && x <= n && y >= 1 && y <= m && c[x][y] == '.' && vis[x][y] == 0){
            return 1 ;
        }
        return 0;
    }

    bool ex_check(int x,int y){
        if(x >= 1 && x <= n && y >= 1 && y <= m && c[x][y] == '.'){
            return 1 ;
        }
        return 0;
    }

    queue<p>q1;///火

    void bfs(){
    //    p p1;
    //    p1.x = x;
    //    p1.y = y;
    //    vis[x][y] = 1;
    //    q1.push(p1);
    //    p p2;
    //    p2.x = fx;
    //    p2.y = fy;
        while(!q1.empty()){
            p pp = q1.front();
            q1.pop() ;
            p pz ;
    //        printf("%d %d\n",pp.x,pp.y);
            for(int i = 1; i <= 4 ; i++){
                pz.x = pp.x + des[i][0] ;
                pz.y = pp.y + des[i][1] ;
                if(check(pz.x,pz.y)){
                    if(vis[pz.x][pz.y] == 0)
                        vis[pz.x][pz.y] = vis[pp.x][pp.y] + 1;
                    else{
                        vis[pz.x][pz.y] = min(vis[pz.x][pz.y],vis[pp.x][pp.y] + 1);
                    }
                    q1.push(pz) ;
                }
            }
        }
    }

    struct person {
        int x;
        int y;
        int cnt;
    };

    queue<person>q2;///人
    int ex_bfs(int x,int y){
        person pr;
        pr.x = x;
        pr.y = y;
        pr.cnt = 1;
        q2.push(pr);
        int minn = 1000000;
        while(!q2.empty()){
            person p2 = q2.front();
            q2.pop();
            person pz;
    //        printf("%d %d\n",p2.x,p2.y);
            if(p2.x == 1 '' p2.x == n '' p2.y == 1 '' p2.y == m){
                minn = min(minn,p2.cnt);
                continue;
            }
            for(int i = 1; i <= 4 ; i++){
                pz.x = p2.x + des[i][0];
                pz.y = p2.y + des[i][1];
                pz.cnt = p2.cnt + 1;
                if(ex_check(pz.x,pz.y) && mark[pz.x][pz.y] == 0 && ((vis[pz.x][pz.y] > pz.cnt)'' vis[pz.x][pz.y] == 0)){
                    mark[pz.x][pz.y] = 1;
                    q2.push(pz);
                }
            }
        }
        return minn;
    }

    int main(){
        int t;
        scanf("%d",&t);
        while(t--){
            scanf("%d %d",&n,&m);
            getchar();
            memset(vis,0,sizeof vis);
            memset(mark,0,sizeof mark);

            for(int i = 1; i <= n ; i++){
                for(int j = 1 ; j <= m ; j++){
                    scanf("%c",&c[i][j]);
                    if(c[i][j] == 'J'){
                        c[i][j] = '.';
                        cx = i;
                        cy = j;
                    }
                    if(c[i][j] == 'F'){
                        c[i][j] = '.';
                        vis[i][j] = 1;
                        p pp;
                        pp.x = i;
                        pp.y = j;
                        q1.push(pp);
                    }
                }
                getchar();
            }

            bfs();
    //        for(int i = 1; i <= n ; i++){
    //            for(int j = 1; j <= m ; j++){
    //                printf("%d",vis[i][j]);
    //            }
    //            printf("\n");
    //        }
            int z = ex_bfs(cx,cy);
            if(z == 1000000){
                printf("IMPOSSIBLE\n");
            }
            else{
                printf("%d\n",z);
            }

        }
    }

    /*

    2
    4 4
    ####
    #JF#
    #..#
    #..#
    3 3
    ###
    #J.
    #.F

    5
    4 4
    ####
    #JF#
    #..#
    #..#
    3 3
    ###
    #J.
    #.F
    4 4
    ####
    #JF#
    #..#
    #..#
    3 3
    ###
    #J.
    #.F
    5 5
    #####
    ..#..
    .J#F.
    ..#..
    #####

    */

<!-- /wp:code -->