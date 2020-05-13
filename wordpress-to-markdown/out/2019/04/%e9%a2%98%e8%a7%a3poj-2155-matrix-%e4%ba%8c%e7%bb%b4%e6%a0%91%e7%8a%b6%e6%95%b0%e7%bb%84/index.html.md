---
layout: post
title: [题解]POJ-2155-Matrix (二维树状数组)
date: 2019-04-12
tags: ["题解"]
---

<!-- wp:paragraph -->

我想说POJ怎么还不完蛋。。。有时候题都交不了，很烦。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 1e4 +10;

    char s[2];
    int a,b,c,d;
    int m,k;
    int cc[maxn][maxn];

    int lowbit(int x) {
        return x&(-x);
    }

    void Not(int x,int y) {
        int j;
        while(x <= m) {
            j = y;
            while(j <= m) {
                cc[x][j]++;
                j += lowbit(j);
            }
            x += lowbit(x);
        }
    }

    int query(int x,int y ) {
        int ans = 0,j;
        while(x >= 1) {
            j = y;
            while(j >= 1) {
                ans += cc[x][j];
                j -= lowbit(j);
            }
            x -= lowbit(x);
        }
        return ans;
    }

    int main() {
        int t;
        scanf("%d",&t);
        while(t--) {
            memset(cc,0,sizeof(cc));
            scanf("%d %d",&m,&k);
            while(k--) {
                scanf("%s",s);
                if(s[0] == 'Q') {
                    scanf("%d %d",&a,&b);
                    printf("%d\n",query(a,b)%2);
                } else {
                    scanf("%d %d %d %d",&a,&b,&c,&d);
                    Not(a,b);
                    Not(c+1,b);
                    Not(a,d+1);
                    Not(c+1,d+1);
                }
            }
            if(t)
                printf("\n");
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

很神奇的玩意，神奇的二进制，为什么最后答案等于query(a,b)%2??????这就要看一篇长达29页的论文了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

文章：《浅谈信息学竞赛中的"0"和"1"--二进制思想在信息学竞赛中的应用》--武森（石家庄二中）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

高中生写的。。。。。。Orz。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

我TM。。。菜

<!-- /wp:paragraph -->