---
layout: post
title: [专题二：搜索进阶]HDU-3567-Eight II-hash+康托+bfs打表
date: 2019-06-03
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    因为一点小问题，vis[pl] = 1，写成了vis[pz] = 1，一直WA。。。。。。。。。。。。。。。。。。。

    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <queue>
    #include <stack>
    using namespace std;
    const int maxn = 5e5 + 10;

    //int des[4][2] = {{0,1},{0,-1},{1,0},{-1,0}};
    int des[4][2] = {{1,0},{0,-1},{0,1},{-1,0}};
    //char ds[4] = {'l','r','u','d'};
    char ds[4] = {'d','l','r','u'};
    //int dz[4] = {-1,1,-3,3};
    int dz[4] = {-3,1,-1,3};

    struct p {
        int x;
        int y;
        int m[10];
    };

    struct p start,ed;

    int son[11][maxn];
    char dir[11][maxn];
    bool vis[maxn*10];
    char c[1000];
    char c2[1000];
    char c3[2000];
    int xx[11];

    int cantor(p pz) {
        int ans = 0;
        int fac = 40320;
        for(int i = 0 ; i <= 8 ; i++) {
            int cnt = 0;
            for(int j = i + 1; j <= 8 ; j++) {
                if(pz.m[i] > pz.m[j]) {
                    cnt++;
                }
            }
            ans += cnt * fac;
            if(i == 8) {
                return ans;
            }
            fac /= 8-i;
        }
    }

    bool check(int x,int y) {
        if( x >= 0 && y >= 0 && x <= 2 && y <= 2 )
            return 1;
        return 0;
    }

    void bfs(int id,p pl) {
        memset(vis,0,sizeof vis);
        p pz,pp;
        queue<p>q;
        q.push(pl);
        int can1,can2;
        can1 = cantor(pl);
        vis[can1] = 1;
        while(!q.empty()) {
            pz = q.front();
            q.pop();
            can1 = cantor(pz);
            for(int i = 0 ; i < 4 ; i++) {
                pp = pz;
                pp.x += des[i][0];
                pp.y += des[i][1];
                if(!check(pp.x,pp.y)) {
                    continue;
                }
                int pos = pp.x * 3 + pp.y;
                swap(pp.m[pos],pp.m[pos+dz[i]]);
                can2 = cantor(pp);
                if(!vis[can2]) {
                    vis[can2] = 1;
    //                printf("%d %c>>\n",can2,ds[i]);
                    dir[id][can2] = ds[i];
                    son[id][can2] = can1;
                    q.push(pp);
                }
            }
        }
    }

    void Preprocessing() {
        p t;
        for(int i = 0 ; i < 9 ; i++) {
            t.m[i] = i + 1;
        }
        for(int i = 0 ; i < 9 ; i++) {
            if(i)
                t.m[i-1] = i;
            t.m[i] = 0;
            t.x = i/3;
            t.y = i%3;
    //        for(int j = 0 ; j <= 8 ; j++){
    //            printf("%d ",t.m[j]);
    //        }
    //        printf("\n");
            bfs(i,t);
        }

    }

    int main() {

        Preprocessing();

        int tt;
        scanf("%d",&tt);
        getchar();
        int id;
        for(int t = 1 ; t <= tt ; t ++) {
            gets(c);
            int cnt = 0;
            for(int i = 0 ; i < strlen(c) ; i++) {
                if(c[i] >= 49 && c[i] <= 57) {
                    start.m[cnt++] = c[i] - 48;
                } else if(c[i] == 'X')
                    start.m[cnt++] = 0;
            }

            for(int i = 0 ; i < 9 ; i++) {
                if(start.m[i]) {
                    xx[start.m[i]] = i+1 ;
                    start.m[i] = i+1 ;
                } else {
                    id = i;
                }
            }

            gets(c2);
    //        printf("%s\n%s\n",c,c2);
            cnt = 0;
            for(int i = 0 ; i < strlen(c2) ; i++) {
                if(c2[i] >= 49 && c2[i] <= 57) {
                    ed.m[cnt++] = (c2[i] - 48);
                } else if(c2[i] == 'X')
                    ed.m[cnt++] = 0;
            }

            for(int i = 0 ; i < 9 ; i++) {
                if(ed.m[i]) {
                    ed.m[i] = xx[ed.m[i]];
                }
            }

            for(int i = 0 ; i < 9 ; ++i){
                printf("%d",start.m[i]);
            }
            printf("\n");
               for(int i = 0 ; i < 9 ; ++i){
               printf("%d",ed.m[i]);
            }
            printf("\n");
            printf("%d>>",id);
    }

    /*

    4
    12X453786
    12345678X
    564178X23
    7568X4123
    12X453786
    12345678X
    564178X23
    7568X4123
    */

<!-- /wp:code -->