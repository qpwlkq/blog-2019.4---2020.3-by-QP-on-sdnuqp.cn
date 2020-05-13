---
layout: post
title: [专题二：搜索进阶]HDU-3085-Nightmare Ⅱ-双向BFS
date: 2019-06-03
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <algorithm>
    #include <cstring>
    #include <queue>
    using namespace std;
    const int maxn = 810;

    int n,m;
    char c[maxn][maxn];
    bool vis[2][maxn][maxn];
    int ghost[3][2];
    int mx,my;
    int gx,gy;
    int flag;
    int dir[5][2] = {0,0, 0,1 ,0,-1, 1,0, -1,0};

    struct node {
        int x;
        int y;
    };
    queue <node> q[2];

    bool judge(int x,int y, int time){
        if(abs(x - ghost[1][0]) + abs(y - ghost[1][1]) <= 2 * time)
            return 0;
        if(abs(x - ghost[0][0]) + abs(y - ghost[0][1]) <= 2 * time)
            return 0;
        return 1;
    }

    bool bfs(int id ,int time){
        int len = q[id].size();
        node p,t;
        while(len--){
            p = q[id].front();
            q[id].pop();
            if(!judge(p.x,p.y,time)){
                continue;
            }
            for(int i = 0; i <= 4 ; i++){
                t.x = p.x + dir[i][0];
                t.y = p.y + dir[i][1];
                if(t.x >= 1 && t.x <= n && t.y >= 1 && t.y <= m && c[t.x][t.y] != 'X' && c[t.x][t.y] != 'Z' && vis[id][t.x][t.y] == 0 && judge(t.x,t.y,time)){
                    vis[id][t.x][t.y] = 1;
                    if(vis[!id][t.x][t.y] == 1){
                        return 1;
                    }
                    q[id].push(t);
                }
            }
        }
        return 0;
    }

    void solve(){
        while(!q[0].empty()){
            q[0].pop();
        }
        while(!q[1].empty()){
            q[1].pop();
        }

        node p;
        p.x = mx;
        p.y = my;
        vis[0][p.x][p.y] = 1;
        q[0].push(p);

        p.x = gx;
        p.y = gy;
        vis[1][p.x][p.y] = 1;
        q[1].push(p);

        int time = 0;
        flag = 0;
        while(!q[0].empty() '' !q[1].empty()){
            time++;
            for(int i = 1; i <= 3 ; i++){
                if(bfs(0,time)){
                    printf("%d\n",time);
                    return ;
                }
            }
            if(bfs(1,time)){
                printf("%d\n",time);
                return ;
            }
        }
        printf("-1\n");
    }

    int main(){
        int t;
        scanf("%d ",&t);
        while(t--){
            scanf("%d %d",&n,&m);
            getchar();
            memset(vis,0,sizeof vis);
            memset(ghost,0,sizeof ghost);
            for(int i = 1 ; i <= n ; i++){
                scanf("%s",c[i]+1);
            }
            for(int i = 1; i <= n ; i++){
                for(int j = 1; j <= m ; j++){
                    if(c[i][j] == 'Z'){
                        if(ghost[0][0] == 0){
                            ghost[0][0] = i;
                            ghost[0][1] = j;
                        }
                        else{
                            ghost[1][0] = i;
                            ghost[1][1] = j;
                        }
                    }
                    if(c[i][j] == 'G'){
                        gx = i;
                        gy = j;
                    }
                    if(c[i][j] == 'M'){
                        mx = i;
                        my = j;
                    }
                }
            }

            solve();
        }
        return 0;
    }

    /*

    3
    5 6
    XXXXXX
    XZ..ZX
    XXXXXX
    M.G...
    ......
    5 6
    XXXXXX
    XZZ..X
    XXXXXX
    M.....
    ..G...

    10 10
    ..........
    ..X.......
    ..M.X...X.
    X.........
    .X..X.X.X.
    .........X
    ..XX....X.
    X....G...X
    ...ZX.X...
    ...Z..X..X

    */

<!-- /wp:code -->