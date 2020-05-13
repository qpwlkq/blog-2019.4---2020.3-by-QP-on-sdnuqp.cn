---
layout: post
title: HYSBZ-1085-骑士精神-IDA_Star(DFS)
date: 2019-06-03
tags: ["题解"]
---

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int ans;
    char c[6][6];
    int m[6][6];
    int mz[6][6];
    int mm[6][6] = {
        0,0,0,0,0,0,
        0,1,1,1,1,1,
        0,0,1,1,1,1,
        0,0,0,2,1,1,
        0,0,0,0,0,1,
        0,0,0,0,0,0
    };

    int des[9][2] = {{0,0},{1,2},{1,-2},{-1,2},{-1,-2},{2,1},{2,-1},{-2,-1},{-2,1}};

    int check() {
        int cnt = 0;
        for(int i = 1; i <= 5 ; i++) {
            for(int j = 1 ; j <= 5 ; j++) {
                if(m[i][j] != mm[i][j]) {
                    cnt++;
                }
            }
        }
        return cnt;
    }

    void A_Star(int x,int y,int w,int en) {
        if(w == en) {
            if(!check()) {
                ans = w;
            }
            return;
        }
        for(int i = 1 ; i <= 8 ; i++) {
            int xx = x + des[i][0];
            int yy = y + des[i][1];
            if(xx >= 1 && yy >= 1 && xx <= 5 && yy <= 5) {
                swap(m[x][y],m[xx][yy]);
                if(check() + w <= en) {
                    A_Star(xx,yy,w+1,en);
                }
                swap(m[x][y],m[xx][yy]);
            }
        }
    }

    int main() {
        int tt;
        scanf("%d",&tt);
        int xx,yy;
        getchar();
        for(int t = 1 ; t <= tt ; t++) {
            for(int i = 1; i <= 5 ; i++) {
                for(int j = 1; j <= 5 ; j++) {
                    scanf("%c",&c[i][j]);
                    if(c[i][j] == '*') {
                        m[i][j] = 2;
                        xx = i;
                        yy = j;
                    } else
                        m[i][j] = c[i][j] - 48;
                }
                getchar();
            }
    //        for(int i =1 ; i<= 5 ; i++) {
    //            for(int j = 1 ; j<= 5 ; j++) {
    //                printf("%d ",m[i][j]);
    //            }
    //            printf("\n");
    //        }
            ans = -1;
            for(int i = 0 ; i <= 15 ; i++) {
                A_Star(xx,yy,0,i);
                if(~ans)
                    break;
            }
            printf("%d\n",ans);
        }
        return 0;
    }

    /*

    2
    10110
    01*11
    10111
    01001
    00000
    01011
    110*1
    01110
    01010
    00100

    */

<!-- /wp:code -->