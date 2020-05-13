---
layout: post
title: [专题一：简单搜索]POJ-3279-Fliptile-二进制枚举
date: 2019-05-19
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    using namespace std;

    int m,n;
    int a[20][20];
    int mp[20][20];
    int vis[20][20];
    int fl[20];
    int fg;

    void mark(int x,int y,int mp[][20]) {
        if(x >= 0 && x < m && y >= 0 && y < n) {
            mp[x][y] = 1 - mp[x][y];
        }
    }

    void check_it(int x,int y,int mp[][20]) {
        vis[x][y] = 1;
        mark(x,y,mp);
        mark(x-1,y,mp);
        mark(x+1,y,mp);
        mark(x,y+1,mp);
        mark(x,y-1,mp);
    }

    int main() {
        scanf("%d %d",&m,&n);
        for(int i = 0;  i < m; i++) {
            for(int j = 0; j < n ; j++) {
                scanf("%d",&a[i][j]);
            }
        }

        int ll = 1 ;
        for(int i = 0; i < (1 << n) ; i++) {
            for(int j = 0 ; j < n ; j++) {
                if(i & (1 << j)) {
                    fl[j] = 1;
                } else
                    fl[j] = 0;
            }

            for(int j = 0 ; j < m ; j++) {
                for(int k = 0 ; k < n ; k++) {
                    mp[j][k] = a[j][k];
                }
            }

            for(int j = 0 ; j < n ; j++) {
                if(fl[j]) {
                    check_it(0,j,mp);
                }
            }

    //        printf("<<<\n");
    //        for(int j = 0 ; j < n ; j++) {
    //            printf("%d ",fl[j]);
    //        }
    //        printf("\n");
    //        printf(">>\n");
    //
    //        for(int j = 0 ; j < m ; j++) {
    //            for(int k = 0; k < n ; k++) {
    //                printf("%d ",mp[j][k]);
    //            }
    //            printf("\n");
    //        }
    //        printf("<>\n");

            for(int j = 1 ; j < m ; j++) {
                for(int k = 0 ; k < n ; k++) {
                    if(mp[j-1][k] == 1) {
                        check_it(j,k,mp);
                    }
                }
            }

    //        for(int j = 0 ; j < m ; j++) {
    //            for(int k = 0; k < n ; k++) {
    //                printf("%d ",mp[j][k]);
    //            }
    //            printf("\n");
    //        }
    //        printf("<>\n");

            int zl = 1;

            for(int j = 0 ; j < n ; j++) {
                if(mp[m-1][j] == 1) {
                    zl = 0;
                }
            }

    //        printf("(%d)\n",zl);
    //        for(int j = 0 ; j < m ; j++) {
    //            for(int k = 0; k < n ; k++) {
    //                printf("%d ",mp[j][k]);
    //            }
    //            printf("\n");
    //        }
    //        printf("<>\n");

            if(zl == 0) {
                memset(vis,0,sizeof vis);
                continue;
            } else {
                ll = 0;
            }
            if(ll == 0) {
                for(int j = 0 ; j < m ; j++) {
                    for(int k = 0 ; k < n ; k++) {
                        printf(k == n-1?"%d":"%d ",vis[j][k]);
                    }
                    printf("\n");
                }
                break;
            } else {
                memset(vis,0,sizeof vis);
            }
        }
        if(ll) {
            printf("IMPOSSIBLE");
        }
        return 0;
    }

    /*
    4 2
    1 1
    1 0
    0 0
    0 0
    */

<!-- /wp:code -->