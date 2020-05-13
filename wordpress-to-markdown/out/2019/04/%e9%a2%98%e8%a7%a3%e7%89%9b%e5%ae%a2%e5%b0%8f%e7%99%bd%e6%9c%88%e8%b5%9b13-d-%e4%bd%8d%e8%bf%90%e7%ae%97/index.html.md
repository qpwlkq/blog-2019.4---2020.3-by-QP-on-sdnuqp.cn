---
layout: post
title: [题解]牛客小白月赛13-D-位运算
date: 2019-04-15
tags: ["题解"]
---

<!-- wp:paragraph -->

这个题冥思苦想也没做出来  

最后看了别人题解，才明白原来前缀和还可以这样用！

<!-- /wp:paragraph -->

<!-- wp:code -->

    AC code:
    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 5e6 + 10;

    int a[maxn],b[maxn],c[maxn];

    int main(){
        int n;
        scanf("%d",&n);
        for(int i = 1 ; i <= n ; i++){
            scanf("%d",&a[i]);
        }
        for(int i = 1 ; i <= n ; i++){//求前i个元素'运算结果
            b[i] = b[i-1] ' a[i];
        }
        for(int i = n ; i >= 1 ; i--){//求第i到n个元素'运算结果
            c[i] = c[i+1] ' a[i];
        }
        int maxx  = 0 ;
        for(int i = 1 ; i <= n ; i++){//遍历第i个不要，求max.
            maxx = max(maxx , b[i-1] ' c[i+1]);
        }
        printf("%d",maxx);
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

前缀和并不一定是前多少个元素相加，还可以是',*之类的，思维要扩出去啊。  
 了解这个后，题就很简单了，就不多赘述了。

<!-- /wp:paragraph -->