---
layout: post
title: UVA-10881-Piotr's Ants
date: 2019-07-23
tags: ["OJ__UVA","第一章思维","训练指南","题解"]
---

<!-- wp:paragraph -->

这个题是真的绕，我绕来绕去，顺序排来排去，不会。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

训练指南第一个题，算是序言中的例题，还没进入第一章，就已经阵亡了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

中间关键几行是学的别人的，写的简单，却很晦涩。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    struct node {
        int d;//id
        int s;//位置
        int t;//方向
    }start[10010],End[10010];

    int order[10010];
    int az[10010];

    bool cmp(struct node x, struct node y) {
        return x.s < y.s;
    }

    bool cmp2(struct node x, struct node y) {
        return x.d < y.d;
    }

    int main() {
        int t;
        int L, T, n;
        char c;
        scanf("%d", &t);
        for (int tt = 1; tt <= t; tt++) {
            scanf("%d %d %d", &L, &T, &n);
            for (int i = 1; i <= n; i++) {
                scanf("%d %c",&start[i].s,&c);
                End[i].t = start[i].t = c == 'L' ? -1 : 1;
                start[i].d = i;
                End[i].d = 0;
                End[i].s = start[i].s + T * start[i].t;
            }
    ////////////
            sort(start + 1 ,start + 1 +n,cmp);
            for(int i =1 ; i <= n ; i++){
                order[start[i].d] = i;
            }
            sort(End+1,End+1+n,cmp);
            for(int i = 1; i <= n ; i++){
                if(End[i].s == End[i+1].s){
                    End[i].t = End[i+1].t = 0;
                }
            }
    //////////////
            printf("Case #%d:\n",tt);
            for (int j = 1; j <= n; j ++) {
                int i = order[j];
                if (End[i].s < 0 '' End[i].s > L) {
                    printf("Fell off\n");
                }
                else {
                    printf("%d ",End[i].s);
                    int x = End[i].t;
                    if (x == -1) {
                        printf("L\n");
                    }
                    else if(x == 1) {
                        printf("R\n");
                    }
                    else {
                        printf("Turning\n");
                    }
                }
            }
        }

        return 0;
    }

    /*

    2
    10 1 4
    1 R
    5 R
    3 L
    10 R
    10 2 3
    4 R
    5 L
    8 R

    */

<!-- /wp:code -->