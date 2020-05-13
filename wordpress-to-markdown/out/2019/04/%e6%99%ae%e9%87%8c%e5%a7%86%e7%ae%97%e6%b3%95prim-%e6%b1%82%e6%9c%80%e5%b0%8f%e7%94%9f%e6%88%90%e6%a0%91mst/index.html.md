---
layout: post
title: 普里姆算法(Prim)-求最小生成树(MST)
date: 2019-04-30
tags: ["图论__最小生成树"]
---

<!-- wp:paragraph -->

注意对比克鲁斯卡尔算法!

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

时间复杂度O(n^2)(基础方法：邻接矩阵存图)，优化不会。。。适用于密集图。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

该算法被数个人于不同时间发现，普里姆不是第一个，也不是第二个。。。(别问我为什么以他的名字命名O_O)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

<del>数据结构课本上讲的真的是一坨屎。</del>

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

正文：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

首先，任选一点当作起始点，选哪个都一样。有两个集合，一个U，另一个V(别管课本怎么命名，怎么讲的了！)。 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

U集合存的是已经连起来的点(即当前构建的MST)，V存剩下的点，U刚开始只有一个起始点。 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

图图图图图图图图图图图(课本上的图，网上讲Prim的也都是这张图图，自己去搜吧，各种颜色各种大小都有，真棒！滑稽.jpg)

<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">lowcost[]数组：  

lowcost[i],表示当前构建的MST到i点的权值，如果lowcost[i] == 0，说明i点已经在当前的MST中了。  

if lowcost[i] = INF,意为当前MST到i点无路径(就是没一条线直接连着).</pre>
<!-- /wp:preformatted -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">mst[]数组：  

mst[i],表示V中能直接连上MST的点的有最小权值那一条路径的终点(U中的点)(fuck!看例子),mst[i] == 0表示i点连上了 </pre>
<!-- /wp:preformatted -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">例：当只有一个v1点时，  

MST(U)上只有1个点v1时。  

此时mst[]数组均初始化为1.  

lowcost[2] == 6 ;  

lowcost[3] == 1 ;  

lowcost[4] == 5;  

lowcost[5] == INF;  

lowcost[6] == INF;  

由图可知，(v1和v2)，(v1和v3)，(v1和v4)直接相连，而(v1和v5)，(v1和v6)没有直接相连。  

有最小权值显然是到v3点，连上。  

MST上又两个点了，更新lowbit[]和mst[]数组。  

lowcost[2] == 5;  

lowcost[3] == 0;  

lowcost[4] == 5;  

lowcost[5] == 6;  

lowcost[6] == 4;  

mst[2] == 3;///v2点到MST当前有两条线，(v2,v1)权值为6，(v2,v3)权值为5，显然到v3点权值小，所以mst[2] == 3;  

mst[3] == 0;///v3已经连上了，所以到MST的权值为0  

mst[4] == 1;///v4点到v1和到v3的权值一样，就没必要更新  

mst[5] == 3;  

mst[6] == 3;</pre>
<!-- /wp:preformatted -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">往后自己类推。  

算法思想其实很简单，一个贪心策略而已，关键是他的算法很巧妙，我只会自己用暴力写出这颗MST来，囧rz。  

滑稽.jpg.</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->

好了code来了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int INF = 0x3f3f3f3f;
    const int maxn = 1000 + 10;

    int n;
    int G[maxn][maxn];
    int lowcost[maxn];
    int mst[maxn];

    int Prim(int sum,int G[][maxn]){
        for(int i = 1 ; i <= n ; i++){///初始化mst数组和lowcost数组
            mst[i] = 1;
            lowcost[i] = G[1][i];
        }
        mst[1] = 0;
        ///
        int min_value , min_id;
        for(int i = 2 ; i <= n ; i++){
            min_value = INF;
            min_id = 0;
            for(int j = 2 ; j <= n ; j++){
                if(min_value > lowcost[j] && lowcost[j] != 0){
                    min_value = lowcost[j];
                    min_id = j;
                }
            }
            ///
            cout<< "从点v" << mst[min_id] << "到点v" << min_id << "  权值 = " << min_value <<'\n';
            ///mst数组记录上一个点(U中),以便输出路径,mst数组作用在此体现。
            ///
            sum += min_value;
            lowcost[min_id] = 0;
            for(int j = 2 ; j <= n ; j++){///真暴力啊。
                if(lowcost[j] > G[min_id][j]){
                    lowcost[j] = G[min_id][j];
                    mst[j] = min_id;
                }
            }
        }
        return sum;
    }

    int main(){
        int t;
        scanf("%d %d",&n,&t);///n个点,t条边
        ///
        for(int i = 1 ; i <= n ; i++){///初始化图G
            for(int j = 1 ; j <= n ; j++){
                G[i][j] = INF;
            }
        }
        ///
        int a,b,c;
        for(int i = 1; i <= t ; i++){///更新数据
            scanf("%d %d %d",&a,&b,&c);
            G[a][b] = c;
            G[b][a] = c;
        }
        ///
    //    for(int i = 1; i <= n ; i++){///输出图,检测是否正确
    //        for(int j = 1; j<= n ;j++){
    //            printf("%d ",G[i][j]);
    //        }
    //        printf("\n");
    //    }
        ///
        cout<<"路径:\n";
        int z = Prim(0,G);
        ///
        cout<<"MST_value = "<<z<<'\n';
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

学会了之后，最好自己敲一遍，因为我的代码习惯和大多数人不同，所以我看别人的博客明白后，自己敲了我自己的风格的代码，舒服。。。。。

<!-- /wp:paragraph -->