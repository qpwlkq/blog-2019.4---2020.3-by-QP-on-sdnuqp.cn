---
layout: post
title: [专题一：简单搜索]POJ-2251-Dungeon Master-BFS
date: 2019-05-16
tags: ["kuangbin专题","题解"]
---

<!-- wp:paragraph -->

刚开始忘记将搜过的点标记为0了，MLE。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <queue>
    using namespace std;

    int L,R,C;
    int zz,xx,yy;
    int maxx;
    int c[35][35][35];
    bool vis[35][35][35];
    int des[7][3] = {{0,0,0},{0,1,0},{0,-1,0},{1,0,0},{-1,0,0},{0,0,1},{0,0,-1}};
    struct p {
        int z;
        int x;
        int y;
        int sum;
    };
    queue<p>q;

    bool check(p pq) {
        if(vis[pq.z][pq.x][pq.y] == 1 && pq.x <= R && pq.x >= 1 && pq.y <= C && pq.y >= 1 && pq.z >= 1 && pq.z <= L) {
            return 1;
        } else
            return 0;
    }

    void bfs() {
        while(!q.empty()) {
            p ppp;
            p pp = q.front();
            q.pop();
            if(pp.x == xx && pp.y == yy && pp.z == zz) {
                maxx = pp.sum;
                return;
            }
            for(int i = 1 ; i <= 6 ; i++) {
                ppp.z = pp.z + des[i][0];
                ppp.x = pp.x + des[i][1];
                ppp.y = pp.y + des[i][2];
                ppp.sum = pp.sum + 1;
                if(check(ppp) == 1) {
                    q.push(ppp);
                    vis[ppp.z][ppp.x][ppp.y] = 0;
                }
            }
        }
        return ;
    }

    int main() {
        while(scanf("%d %d %d",&L,&R,&C)!=EOF && (L''R''C)) {
            maxx = 10000;
            getchar();
            for(int k = 1; k <= L ; k++) {
                for(int i = 1; i <= R ; i++) {
                    for(int j = 1 ; j <= C ; j++) {
                        scanf("%c",&c[k][i][j]);
                        if(c[k][i][j] == 'S') {
                            p pp;
                            pp.x = i;
                            pp.y = j;
                            pp.z = k;
                            pp.sum = 0;
                            q.push(pp);
                            c[k][i][j] = '.';
                        }
                        if(c[k][i][j] == 'E') {
                            c[k][i][j] = '.';
                            zz = k;
                            xx = i;
                            yy = j;
                        }
                        if(c[k][i][j] == '.') {
                            vis[k][i][j] = 1;
                        } else
                            vis[k][i][j] = 0;
                    }
                    getchar();
                }
                getchar();
            }
            bfs();
            while(!q.empty()) {
                q.pop();
            }

            printf(maxx == 10000?"Trapped!\n":"Escaped in %d minute(s).\n",maxx);

        }
        return 0;
    }

<!-- /wp:code -->