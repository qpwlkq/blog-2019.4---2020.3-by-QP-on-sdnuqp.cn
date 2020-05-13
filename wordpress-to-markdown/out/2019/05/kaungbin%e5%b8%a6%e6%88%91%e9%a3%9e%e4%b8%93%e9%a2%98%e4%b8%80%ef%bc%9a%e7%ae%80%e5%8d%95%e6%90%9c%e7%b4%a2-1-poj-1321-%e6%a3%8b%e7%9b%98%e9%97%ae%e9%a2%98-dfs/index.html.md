---
layout: post
title: [专题一：简单搜索]POJ-1321-棋盘问题-DFS
date: 2019-05-16
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    //#include <bits/stdc++.h>
    using namespace std;

    int n,k;
    int cnt;
    char c[10][10];
    bool vis[10][10];
    bool cc[10];

    void dfs(int x,int way){
        if(way == k){
            cnt++;
            return ;
        }
        if(x > n)
            return ;
        for(int i = 1; i <= n ; i++){
            if(c[x][i] == '#' && cc[i] == 0){
                cc[i] = 1;
                dfs(x+1,way+1);
                cc[i] = 0;
            }
        }
        dfs(x+1,way);
    }

    int main(){
        char chr;
        while(scanf("%d %d",&n,&k)!=EOF){
            if(n == -1 && k == -1){
                break;
            }
            cnt = 0;
            getchar();
            for(int i = 1 ; i <= n ; i++){
                for(int j = 1 ; j <= n ; j++){
                    scanf("%c",&chr);
                    c[i][j] = chr;
                    if(chr == '#'){
                        vis[i][j] = 1;
                    }
                    else{
                        vis[i][j] = 0;
                    }
                }
                getchar();
            }
            dfs(0,0);
            printf("%d\n",cnt);
        }
        return 0;
    }

<!-- /wp:code -->