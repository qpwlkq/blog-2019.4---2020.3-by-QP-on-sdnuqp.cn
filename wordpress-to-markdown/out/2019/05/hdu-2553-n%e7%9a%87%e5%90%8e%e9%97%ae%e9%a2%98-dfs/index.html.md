---
layout: post
title: HDU-2553-N皇后问题-DFS
date: 2019-05-09
tags: ["题解"]
---

<!-- wp:paragraph -->

这个题是个基础DFS深搜  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

但是这个题有个坑。  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

别看它给了N <= 10 ,他问的可不只10次。。。。直接1到10打表存在数组里，他问什么O(1)复杂度直接输出。  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

秒过！，不然测试样例大概是问了你很多很多次N=10的时候。。。。。于是超时。。。。太TM奸诈了!?  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题好久之前，刚学DFS和BFS时做的，那时我单独把10拿了出来才A了。。。。没想到啊，出题人如此奸诈，Orz.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

r_c[ ]数组：标记左斜；

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

c_r[ ]数组：标记右斜；

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

col[ ]数组：标记列；

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

从第一行往下深搜，所以不用标记行，每一次递推，就是往下移动一行，不用多说了吧，很简单那。

<!-- /wp:paragraph -->

<!-- wp:code -->

    /*
    N皇后问题
    */
    #include <bits/stdc++.h>
    using namespace std;

    int num[11];
    int sum;
    int N;
    int way;
    int col[25];
    int c_r[25];
    int r_c[25];

    void DFS(int n){
        if(way == N){
            sum++;
            return;
        }
        if(n > N){
            return ;
        }
        for(int i = 1; i <= N ; i++){
            if(!col[i] && !c_r[N + n - i] && !r_c[i+n]){
                col[i] = 1;
                c_r[N+n-i] = 1;
            r_c[i+n] = 1;
                way++;
                DFS(n+1);
                col[i] = 0;
                c_r[N+n-i] = 0;
            r_c[i+n] = 0;
                way--;
            }
        }
    }

    int main(){
        ios::sync_with_stdio(0);

        for(int i = 1; i <= 10 ; i++){
            N = i;
            sum = 0;
            way = 0;
            memset(col,0,sizeof col);
            memset(r_c,0,sizeof r_c);
            memset(c_r,0,sizeof c_r);
            DFS(1);
            num[i] = sum;
        }
        while(cin>>N && N){
            cout<<num[N]<<'\n';
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

<!-- /wp:paragraph -->