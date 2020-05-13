---
layout: post
title: [题解]HDU-1556-Color the ball (前缀和||树状数组||线段树)
date: 2019-04-11
tags: ["数据结构__树状数组","数据结构__线段树"]
---

<!-- wp:paragraph -->

这道题并不是单纯的模板题，我敲了一个模板就交了，结果肯定超时了，树状数组处理区间单点数值的问题，不能单纯用基础模板。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

树状数组练习：https://vjudge.net/contest/287770#problem/C

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

前缀和 '' 树状数组 '' 线段树 都可以做

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

1-前缀和：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

只是对区间开头和结尾进行处理，太巧妙了，想不到啊！！！Orz

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码：  

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 1e5 +10;

    int c[maxn];

    int main(){
        int l;
        int n,m;
        int ans;
        while(~scanf("%d",&l)&&l){
            memset(c,0,sizeof c);
            for(int j = 1 ; j <= l ; j++){
                scanf("%d%d",&n,&m);
                c[n]++;
                c[m+1]--;
            }
            ans = 0;
            for(int i = 1 ; i <= l ; i++){
                ans += c[i];
                printf("%d",ans);
                printf(i != l?" ":"\n");
            }
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

2 - 树状数组

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 1e5 + 10;

    int c[maxn];
    int sum[maxn];

    int lowbit(int x) {
        return x&(-x);
    }

    int update(int x, int y,int n) {
        while(x <= n) {
            c[x] += y;
            x += lowbit(x);
        }
    }

    int getsum(int x ){
        int ans = 0;
        while(x >= 1){
            ans += c[x];
            x -= lowbit(x);
        }
        return ans;
    }

    int main() {
        int t;
        int n,m;
        int ans;
        while(~scanf("%d",&t)&&t) {
            memset(c,0,sizeof c);

            for(int j = 1 ; j<= t ;j++) {
                scanf("%d %d",&n,&m);
                update(n,1,t);
                update(m+1,-1,t);
            }

            for(int i = 1 ; i <= t ; i++){
                ans = getsum(i);           ///与第一种方法操作相同，都是要求1到当前点的和。
                printf(i == t?"%d":"%d ",ans);
            }
            printf("\n");
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

3 - 线段树

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

刚学了线段树，还是感觉很虚。

<!-- /wp:paragraph -->