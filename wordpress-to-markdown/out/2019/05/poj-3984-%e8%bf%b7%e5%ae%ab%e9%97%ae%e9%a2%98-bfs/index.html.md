---
layout: post
title: [专题一：简单搜索]POJ-3984-迷宫问题-BFS
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <queue>
    using namespace std;

    int n,m;
    int vis[5][5];
    int des[5][2] = {{0,0},{1,0},{-1,0},{0,1},{0,-1}};

    struct p{
        int x;
        int y;
        int pre[50][2];
        int w;
    };
    int maze[5][5];
    bool check(int x,int y){
        if(x >= 0 && x <= 4 && y >= 0 && y <= 4 && vis[x][y] == 0 && maze[x][y] == 0)
            return 1;
        return 0;
    }

    queue<p>q;
    void dfs(){
        p p1;
        p1.x = 0;
        p1.y = 0;
        p1.w = 0;
        p1.pre[p1.w][0] = p1.x;
        p1.pre[p1.w][1] = p1.y;
        q.push(p1);
        while(!q.empty()){
            p pp ;
            pp = q.front();
            q.pop();
    //        printf("%d %d\n",pp.x,pp.y);
            if(pp.x == 4 && pp.y == 4){
                for(int i = 0 ; i <= pp.w ; i++){
                    printf("(%d, %d)\n",pp.pre[i][0],pp.pre[i][1]);
                }
            }
            p pz;
            for(int i = 1;  i <= 4 ; i++){
                pz = pp;
                pz.w = pp.w + 1;
                pz.x = pp.x + des[i][0];
                pz.y = pp.y + des[i][1];
                pz.pre[pz.w][0] = pz.x;
                pz.pre[pz.w][1] = pz.y;
                if(check(pz.x,pz.y)){
                    vis[pz.x][pz.y] = 1;
                    q.push(pz);
                }
            }
        }
    //    printf("OK\n");
    }

    int main() {
        for(int i = 0 ; i < 5 ; i++){
            for(int j= 0 ; j < 5 ; j++){
                scanf("%d",&maze[i][j]);
            }
        }
        dfs();
    }

<!-- /wp:code -->