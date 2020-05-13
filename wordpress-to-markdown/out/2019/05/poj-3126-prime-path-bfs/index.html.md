---
layout: post
title: [专题一：简单搜索]POJ-3126-Prime Path-BFS
date: 2019-05-19
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    //#include <bits/stdc++.h>
    #include <cstdio>
    #include <queue>
    #include <algorithm>
    #include <cstring>
    using namespace std;

    int a,b;
    int n;
    int prime[10010];
    int vis[10010];

    struct p {
        int num;
        int id;
    };

    void isprime() {
        for(int i = 2 ; i <= 10000 ; i++) {
            if(prime[i] == 0) {
                for(int j = 2 * i ; j <= 10000 ; j += i) {
                    prime[j] = 1;
                }
            }
        }
    }

    queue<p>q;

    int bfs(int x) {
        p pz;
        pz.num = x;
        pz.id = 0;
        q.push(pz);
        int nm;
        while(!q.empty()) {
            p z = q.front();
            q.pop();

            if(z.num == b) {
                printf("%d\n",z.id);
                while(!q.empty()) {
                    q.pop();
                }
                return 1;
            }

            nm = z.num % 10;
            for(int i = 1 ; i <= 9 - nm ; i++) {
                if(!prime[z.num + i] && !vis[z.num + i]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i;
                    vis[z.num + i] = 1 ;
                    q.push(zz);
                }
            }

            nm = z.num / 10 % 10 ;
            for(int i = 1 ; i <= 9 - nm ; i++) {
                if(!prime[z.num + i * 10] && !vis[z.num + i * 10]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i * 10;
                    vis[z.num + i * 10] = 1;
                    q.push(zz);
                }
            }

            nm = z.num / 100 % 10 ;
            for(int i = 1 ; i <= 9 - nm ; i++) {
                if(!prime[z.num + i * 100] && !vis[z.num + i * 100]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i * 100;
                    vis[z.num + i * 100] = 1;
                    q.push(zz);
                }
            }

            nm = z.num / 1000;
            for(int i = 1 ; i <= 9 - nm ; i++) {
                if(!prime[z.num + i * 1000] && !vis[z.num + i * 1000]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i * 1000;
                    vis[z.num + i * 1000] = 1;
                    q.push(zz);
                }
            }
            ///
            nm = z.num % 10;

    //        printf(">>>\n");
            for(int i = 1 ; i < nm ; i++) {
                i *= -1;
                if(!prime[z.num + i] && !vis[z.num + i]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i;
                    vis[z.num + i] = 1 ;
                    q.push(zz);
                }
                i *= -1;
            }

            nm = z.num / 10 % 10 ;
            for(int i = 1 ; i <= nm ; i++) {
                i *= -1;
                if(!prime[z.num + i * 10] && !vis[z.num + i * 10]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i * 10;
                    vis[z.num + i * 10] = 1;
                    q.push(zz);
                }
                i *= -1;
            }

            nm = z.num / 100 % 10 ;
            for(int i = 1 ; i <= nm ; i++) {
                i *= -1;
                if(!prime[z.num + i * 100] && !vis[z.num + i * 100]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i * 100;
                    vis[z.num + i * 100] = 1;
                    q.push(zz);
                }
                i *= -1;
            }

            nm = z.num / 1000;
            for(int i = 1 ; i < nm ; i++) {
                i *= -1;
                if(!prime[z.num + i * 1000] && !vis[z.num + i * 1000]) {
                    p zz = z;
                    zz.id = z.id + 1;
                    zz.num = z.num + i * 1000;
                    vis[z.num + i * 1000] = 1;
                    q.push(zz);
                }
                i *= -1;
            }

            ///

        }
        return 0;
    }

    int main() {
        scanf("%d",&n);
        isprime();
    //    for(int i = 2; i <= 10000 ; i++){
    //        if(!prime[i])
    //            printf("%d\n",i);
    //    }
        for(int i = 1; i <= n ; i++) {
            memset(vis,0,sizeof vis);
            scanf("%d %d",&a,&b);
            if(bfs(a)) {
                ;
            } else {
                printf("IMPOSSIBLE\n");
            }
        }
        return 0;
    }

    /*

    1
    1033 8179

    1
    1373 8017

    */

<!-- /wp:code -->