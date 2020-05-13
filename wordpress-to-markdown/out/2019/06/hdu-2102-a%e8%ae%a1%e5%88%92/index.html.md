---
layout: post
title: [专题二：搜索进阶]HDU-2102-A计划-BFS
date: 2019-06-03
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    这题只是简单BFS，应该放在上一个专题吧。。。

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 10 + 1;

    int m,n,z;
    char c[2][maxn][maxn];
    int mark_map[2+1][maxn+1][maxn+1];
    int dir[5][2] = {{0,0},{1,0},{-1,0},{0,1},{0,-1}};

    int position_princess_x;
    int position_princess_y;
    int position_princess_z;

    struct node {
        int x;
        int y;
        int z;
        int sum;
    };

    bool check(int x, int y, int z){
        if(x >= 0 && x < m && y >= 0 && y < n && z >= 0 && z < 2 && mark_map[z][x][y] == 0){
            return 1;
        }
        return 0;
    }

    queue <node >q;
    void bfs(){
        node p,t;
        p.x = 0;
        p.y = 0;
        p.z = 0;
        p.sum = 0;
        mark_map[p.z][p.x][p.y] = 0;
        q.push(p);
        while(!q.empty()){
            p = q.front();
            q.pop();
            if(p.x == position_princess_x)
                if(p.y == position_princess_y)
                    if(p.z == position_princess_z){
                        printf("YES\n");
                        while(!q.empty()){
                            q.pop();
                        }
                        return ;
                    }
            if(p.sum >= z)
                continue;
            for(int i = 1 ; i <= 4 ; i++){
                t.x = p.x + dir[i][0];
                t.y = p.y + dir[i][1];
                t.z = p.z;
                t.sum = p.sum + 1;
                if(check(t.x, t.y, t.z)){
                    if(c[t.z][t.x][t.y] == '.'){
                        mark_map[t.z][t.x][t.y] = 1;
                        q.push(t);
                    }
                    else if(c[t.z][t.x][t.y] == '#'){
                        if(c[1-p.z][t.x][t.y] == '.' && mark_map[1-p.z][t.x][t.y] == 0){
                            t.z = 1 - p.z ;
                            mark_map[t.z][t.x][t.y] = 1;
                            mark_map[1-p.z][t.x][t.y] = 1;
                            q.push(t);
                        }
                    }
                }
            }
        }
        printf("NO\n");
        return ;
    }

    int main() {
        int t;
        scanf("%d",&t);
        while(t--) {
            memset(mark_map,0,sizeof mark_map);
            scanf("%d %d %d",&m,&n,&z);
            getchar();
            for(int k = 0 ; k < 2 ; k++) {
                for(int i = 0 ; i < m ; i++) {
                    for(int j = 0 ; j < n ; j++) {
                        scanf("%c",&c[k][i][j]);
                        if(c[k][i][j] == 'P'){
                            position_princess_x = i;
                            position_princess_y = j;
                            position_princess_z = k;
                            c[k][i][j] = '.';
                        }
                    }
                    getchar();
                }
                !k?getchar():1;
            }
    //        printf("\n>>>>\n");
    //        for(int i = 0 ; i < 2 ; i++){
    //            for(int j = 0 ; j < m ; j++){
    //                printf("%s \n",c[i][j]);
    //            }
    //            printf("\n");
    //        }

            bfs();

        }
        return 0;
    }

<!-- /wp:code -->