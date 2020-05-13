---
layout: post
title: 迪杰斯特拉算法(Dijkstra)
date: 2019-05-09
tags: ["数据结构__基础","算法"]
---

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 100 + 10;
    const int INF = 0x3f3f3f3f;

    int edge[maxn][maxn];
    int dis[maxn];
    int vis[maxn];

    void Trausal(int *dis,int n);

    void Dijkstra(int edge[][maxn],int n) {
        int minn;
        int id ;
        for(int i = 1; i < n ; i++) {
            minn = INF;
            for(int j = 1; j <= n; j++) {
                if(vis[j] == 0 && dis[j] < minn) {
                    minn = dis[j];
                    id = j;
                }
            }
            if(minn == INF) {
                break;
            }
            vis[id] = 1;
            for(int j = 1; j <= n; j++)
                if(vis[j] == 0)
                    dis[j] = min(dis[j],dis[id] + edge[id][j]);
        }
    //    Trausal(dis,n);
        printf("%d\n",dis[n]);
    }

    void Trausal(int *dis,int n) {
        printf(">>>>>");
        for(int i = 1 ; i <= n ; i++) {
            printf(" %d ",dis[i]);
        }
        printf("<<<<<<\n");
    }

    int main() {
        int n,m;
        int a,b,c;
        while(~scanf("%d %d",&n,&m) && (n '' m) ) {
            memset(vis,0,sizeof vis );
            memset(edge,0x3f,sizeof edge);
            memset(dis,0,sizeof dis);
            for(int i = 1; i <= n ; i++) {
                edge[i][i] = 0;
            }

    //        printf("%d\n",edge[1][2]);
            for(int i = 1; i <= m ; i++) {
                scanf("%d %d %d",&a,&b,&c);
                if(c < edge[a][b]) {//可能有重边，有个题这里我没判重边，WA惨了。
                    edge[a][b] = c;
                    edge[b][a] = c;
                }
            }

            vis[1] = 1;
            for(int i = 1; i <= n; i++) {
                dis[i] = edge[1][i];
            }

            Dijkstra(edge,n);
        }
        return 0 ;
    }

<!-- /wp:code -->