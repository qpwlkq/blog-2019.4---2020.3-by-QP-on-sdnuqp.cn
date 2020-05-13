---
layout: post
title: 排列生成算法
date: 2019-07-26
tags: ["算法"]
---

<!-- wp:paragraph -->

第一种是生成1 ~ n的全排列;

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

第二种适用于无重复数组

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

第三种适用于可重复数组

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

第四种是 解答树

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

第五种是 库函数（next_permutation()）(生成下一个排列)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

刘汝佳大牛的代码，打下来当板子。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 100 + 1;

    int n;
    int A[maxn];
    int P[maxn];

    void print_permutation(int n ,int* A ,int cur) {
        if (cur == n) {
            for (int i = 0; i < n; i++) {
                printf("%d ",A[i]);
            }
            printf("\n");
        }
        else for (int i = 1; i <= n; i++) {
            int ok = 1;
            for (int j = 0; j < cur; j++) {
                if (A[j] == i) {
                    ok = 0;
                }
            }
            if (ok) {
                A[cur] = i;
                print_permutation(n, A, cur + 1);
            }
        }
    }

    void print_permutation(int n ,int* A ,int cur) {
        if (cur == n) {
            for (int i = 0; i < n; i++) {
                printf("%d ",A[i]);
            }
            printf("\n");
        }
        else for (int i = 1; i <= n; i++) {
            int ok = 1;
            for (int j = 0; j < cur; j++) {
                if (A[j] == P[i]) {
                    ok = 0;
                }
            }
            if (ok) {
                A[cur] = P[i];
                print_permutation(n, A, cur + 1);
            }
        }
    }

    void print_permutation(int n ,int * P,int* A ,int cur) {
        if (cur == n) {
            for (int i = 0; i < n; i++) {
                printf("%d ",A[i]);
            }
            printf("\n");
        }
        else
            for (int i = 0; i < n; i++) {
                if (!i '' P[i] != P[i - 1]) {
                    int c1 = 0, c2 = 0;
                    for (int j = 0; j < cur; j++) {
                        if (A[j] == P[i]) c1++;
                    }
                    for (int j = 0; j < n; j++) {
                        if (P[i] == P[j]) c2++;
                    }
                    if (c1 < c2) {
                        A[cur] = P[i];
                        print_permutation(n,P, A, cur+1);
                    }
                }
            }
    }

    int main() {
        scanf("%d", &n);
        for (int i = 0; i < n; i++) {
            scanf("%d", &P[i]);
        }
        sort(P, P + n); /// 用于3
        print_permutation(n,A,0);///用于1，2
        print_permutation(n,P,A,0);///用于3
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

至于解答树和next_permutation函数是什么怎么用，请看紫薯或：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[https://blog.csdn.net/flora715/article/details/80967551](https://blog.csdn.net/flora715/article/details/80967551)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

转载 解答树 code:

<!-- /wp:paragraph -->

<!-- wp:code -->

        #include <string.h>
        #include <iostream>

        using namespace std;
        const int N = 99999999;     //输入排序的个数的最大值
        int record[N];              //记录每次排序的序列
        int visited[N];             //标记节点是否被访问过
        int n;                      //输入节点的数目
        int totalSize = 0;
        void DFS(int start){
            if(start>=n){           //递归出口
                for(int i=0;i<n;i++){
                    cout<<record[i]<<" ";
                }
                totalSize++;
                cout<<endl;
                return;
            }
            for(int i=1;i<=n;i++){      //深度遍历节点，并标记已经访问过的节点
                if(visited[i]==0){
                    visited[i] = 1;
                    record[start] = i;
                    DFS(start+1);       //递归遍历
                    visited[i] = 0;     //回退时标记回退的节点为未被访问节点
                }
            }
        }

        int main()
        {
            cin>>n;
            memset(visited,0,n);
            DFS(0);
            cout<<"totalSize = "<<totalSize<<endl;
            return 0;
        }

<!-- /wp:code -->