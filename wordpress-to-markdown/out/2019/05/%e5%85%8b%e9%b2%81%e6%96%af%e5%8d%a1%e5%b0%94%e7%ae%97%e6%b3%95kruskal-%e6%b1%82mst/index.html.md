---
layout: post
title: 克鲁斯卡尔算法(Kruskal)-求MST
date: 2019-05-04
tags: ["图论__最小生成树"]
---

<!-- wp:paragraph -->

注意对比普里姆算法

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

"加边法"  

时间复杂度O(eloge),e是边数,更适用于稀疏图。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

依然是基于贪心策略的算法。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

推荐讲解：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

https://blog.csdn.net/junya_zhang/article/details/83584592(讲的很好)  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

http://data.biancheng.net/view/41.html(他的讲解也很好，代码就。。太乱了。。柑橘好高级)

<!-- /wp:paragraph -->

<!-- wp:code -->

    code:

    #include <bits/stdc++.h>
    using namespace std;

    struct Point{
        int ver1;
        int ver2;
    //    int edge;
        int weight;
    }a[1010];

    bool cmp(struct Point a, struct Point b){
        return a.weight < b.weight;
    }

    int parent[1010];

    int Find(int z){
        while(parent[z] > 0){
            z = parent[z];
        }
        return z;
    }

    void Kruskal(int _end){
        int n,m;
        for(int i = 1; i <= _end ; i++){
            n = Find(a[i].ver1);
            m = Find(a[i].ver2);
            if(n != m){
                parent[n] = m;
                printf("%d %d %d\n",a[i].ver1,a[i].ver2,a[i].weight);
            }
        }
    }

    int main(){
        int n1,n2;///点数和边数
        scanf("%d %d",&n1,&n2);
        for(int i = 1 ; i <= n2 ; i++){
            scanf("%d %d %d",&a[i].ver1,&a[i].ver2,&a[i].weight);
        }
        sort(a+1,a+1+n2,cmp);

        Kruskal(n2);

        return 0 ;
    }

    /*

    9 15
    5 8 7
    3 9 8
    1 2 10
    1 6 11
    2 9 12
    4 8 16
    2 7 16
    6 7 17
    2 3 18
    7 8 19
    4 5 20
    4 9 21
    3 4 22
    4 7 24
    5 6 26

    */

<!-- /wp:code -->