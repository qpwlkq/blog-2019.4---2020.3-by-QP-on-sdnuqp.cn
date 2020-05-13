---
layout: post
title: [好题!]HDU-5877-Weak Pair-树状数组+DFS+离散化
date: 2019-06-03
tags: ["题解"]
---

<!-- wp:paragraph -->

貌似是16年区域赛大连站的一道题，我们知道DFS要消除后效性，比如：vis[...] = 1,dfs(),vis[...] = 0.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

但这道题没有用这么低级的vis标记，而是与树状数组(或线段树)联系起来!

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

好题，没见过，真的想不到！！！！

<!-- /wp:paragraph -->

<!-- wp:code -->

    /*
    1.树状数组在DFS中在线更新!
    2.k/a[i] 加入要离散化的数组中!
    3.树状数组维护小于a[i]的值的个数!

    */

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 2e5 + 10;

    int t;
    int n;
    long long k;
    long long ans;
    int u,v;
    int a[maxn];    ///记录输入1-N
    int c[maxn];    ///树状数组
    struct node {
        vector <int > child;
    }tree[maxn];

    int mark_root[maxn];///标记根节点

    map <int ,int > vis; ///标记节点的值(离散化时数据不重复)
    vector <int > vec;   ///离散化，利用vec.upperbound(???) - vec.begin()得到离散化后的编号(大佬的离散化,Orz)

    int lowbit(int x){
        return x & -x;
    }

    void update(int x ,int y){
        while(x <= maxn){
            c[x] += y;
            x += lowbit(x);
        }
    }

    int getsum(int x){
        int ans = 0 ;
        while(x >= 1){
            ans += c[x];
            x -= lowbit(x);
        }
        return ans;
    }

    void init(){
        ans = 0L;
        vec.clear();
        vis.clear();
        for(int i = 1 ; i <= maxn ; i++){
            tree[i].child.clear();
            mark_root[i] = 0;
            c[i] = 0;
        }
    }

    void DFS(int x){
        int len = tree[x].child.size();
        int pos = upper_bound(vec.begin(),vec.end(),k/a[x]) - vec.begin();   ///大佬的离散化。。。。
        int posthis = lower_bound(vec.begin(),vec.end(),a[x]) - vec.begin();

        ans += getsum(pos);

        update(posthis + 1,1);

        for(int i = 0 ; i < len ; i++){
            DFS(tree[x].child[i]);
        }
        update(posthis + 1,-1);
    }

    int main() {
        scanf("%d",&t);
        while(t--) {
            init();
            scanf("%d %lld",&n,&k);
            for(int i = 1; i <= n ; i++){
                scanf("%d",&a[i]);
                if(vis[a[i]] == 0){
                    vec.push_back(a[i]);
                    vis[a[i]] = 1 ;
                }
            }

            sort(vec.begin(),vec.end());
            for(int i = 1; i < n ; i++){
                scanf("%d %d",&u,&v);
                mark_root[v] = 1;
                tree[u].child.push_back(v);
            }

            for(int i = 1; i <= n ; i++){
                if(!mark_root[i]){
                    DFS(i);
                    break;
                }
            }
            printf("%lld\n",ans);
        }
    }

<!-- /wp:code -->