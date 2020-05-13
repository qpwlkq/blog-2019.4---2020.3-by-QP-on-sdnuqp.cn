---
layout: post
title: POJ-2481-Cows-树状数组
date: 2019-05-05
tags: ["数据结构__树状数组"]
---

<!-- wp:paragraph -->

我想说，我 TMD 终于把这题过了。。。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这道题并不难，莫名其妙的持续大脑混乱，样例死活不对。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code(附赠几个样例，滑稽.jpg)：

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <algorithm>
    #include <cstring>
    //#include <bits/stdc++.h>
    using namespace std;
    const int maxn = 1e5 + 10;

    int c[maxn];
    int num[maxn];
    int revise[maxn];
    //int vis[maxn];
    struct pp{
        int l;
        int r;
        int id;
    }a[maxn];

    bool cmp(struct pp a,struct pp b){
        if(a.r != b.r)
            return a.r > b.r;
        else
            return a.l < b.l;
    }

    int lowbit(int x){
        return x&(-x);
    }

    void update(int x,int y){
        while(x <= y){
            c[x] += 1;
            x += lowbit(x);
        }
    }

    int getsum(int x){
        int ans = 0;
        while(x >= 1){
            ans += c[x];
            x -= lowbit(x);
        }
        return ans;
    }

    int main(){
        int n;
        int cnt ;
        int z;
        int maxx ;
        while(scanf("%d",&n) && n){
            maxx = -1;
            memset(c,0,sizeof c);
            memset(num,0,sizeof num);
            memset(revise,0, sizeof revise);
    //        memset(vis,0,sizeof vis);
            for(int i = 1 ; i <= n ; i++){
                scanf("%d %d",&a[i].l,&a[i].r);
                a[i].l += 1;
                a[i].r += 1;
                a[i].id = i;
                if(maxx < a[i].r){
                    maxx = a[i].r;
                }
            }
            sort(a+1,a+1+n,cmp);
            for(int i = 1 ; i <= n ; i++){                   /////算有多少相同的区间(看看后面第二个样例)
                if(a[i].l == a[i-1].l && a[i].r == a[i-1].r){
                    if(a[i-1].l == a[i-2].l && a[i-1].r == a[i-2].r){
                        revise[i] = revise[i-1] + 1;
                    }
                    else{
                        revise[i]++;
                    }
                }
            }

            for(int i = 1 ; i <= n ; i++){
    //            if(vis[a[i].l] == 0){
                    update(a[i].l,maxx);
    //                vis[a[i].l] = 1;
    //            }
                z = getsum(a[i].l);
    //            printf("(%d %d)\n",getsum(maxx),getsum(a[i].l));
    //            num[a[i].id] = z-1 ;                
                num[a[i].id] = z-1 - revise[i];      //////// z-1 ：去掉当前点
            }

            for(int i = 1 ; i <= n ; i++){
                printf(i != n+1?"%d ":"%d",num[i]);
            }
            cout<<"\n";
        }
        return 0;
    }

    /*

    3
    1 2
    0 3
    3 4
    0

    7
    3 4
    0 3
    0 3
    0 2
    0 2
    0 2
    1 2
    0

    4
    0 4
    1 2
    0 3
    3 4
    0

    */

<!-- /wp:code -->

<!-- wp:paragraph -->

我刚开始想的是用二维数组的，但是明显的，要用10^10大小的数组，开不了。  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

正确思路应该是先排序，我是以区间右端从大到小排序，然后用区间左端更新区间，求前缀和。  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

思路一定要清晰！代码放这了。

<!-- /wp:paragraph -->