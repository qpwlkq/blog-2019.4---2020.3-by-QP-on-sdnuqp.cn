---
layout: post
title: 高斯消元法
date: 2019-05-05
tags: ["数论__高斯消元"]
---

<!-- wp:paragraph -->

我的依然有很多漏洞的算法：

<!-- /wp:paragraph -->

<!-- wp:code -->

    ///
    #include <bits/stdc++.h>
    using namespace std;
    #define Elemtype double
    const int maxn = 1000;
    const Elemtype eps = 1e-8;
    Elemtype a[maxn][maxn];
    Elemtype vis[maxn];
    int num[maxn];

    void matrix(Elemtype a[][maxn],int n, int m) {
        for(int i = 1 ; i <= n ; i++) {
            for(int j = 1; j <= m ; j++) {
                printf("%f ",a[i][j]);
            }
            printf("\n");
        }
        cout<<"\n";
    }

    void Guass(Elemtype a[][maxn], int n,int m) {
        for(int i = 1 ; i <= n ; i++) {
            if(fabs(a[i][i]) <= eps) {
                continue;
            }

            matrix(a,n,m);
            for(int k = i+1 ; k <= n ; k++) {
                vis[k] = a[k][i]/a[i][i];
            }

            for(int k = i+1 ; k <= n ; k++){
                for(int j = i ; j <= m ; j++){
                    a[k][j] -= vis[k]*a[i][j];
                }
            }
        }
    }

    int solution(Elemtype a[][maxn],int n, int m){
        for(int i = n ; i >= 1; i--){
            for(int j = m-1 ; j >= 1 ; j--){
                if(fabs(a[i][j]) > eps){
                    num[i]++;
                }
            }
        }

    //    for(int i = 1; i <= n ; i++){
    //        printf("%d \n",num[i]);
    //    }
        for(int i = n ; i >= 1 ; i--){
            if(num[i] == 0 && a[i][m] > 0){
                return -1;
            }
            if(num[i] > m-i){
                return 1;
            }
        }

        return 0;
    }

    int main() {
        int n,m ;
        scanf("%d %d",&n,&m);
        for(int i = 1; i <= n ; i++) {
            for(int j = 1 ; j <= m ; j++) {
                scanf("%lf",&a[i][j]);
            }
        }
        cout<<"\n";

        Guass(a,n,m);

        int flag = solution(a,n,m);

        if(flag > 0){
            printf("有无数个解");
        }
        else if(flag < 0){
            printf("无解");
        }
        else{
            printf("有解");
        }
        return 0;
    }

    /*

    3 3
    1 1 2
    1 -2 -1
    0 1 2

    */

<!-- /wp:code -->