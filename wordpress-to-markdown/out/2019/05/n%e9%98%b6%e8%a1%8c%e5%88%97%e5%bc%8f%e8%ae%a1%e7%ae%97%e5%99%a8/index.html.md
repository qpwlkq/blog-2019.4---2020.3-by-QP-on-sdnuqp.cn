---
layout: post
title: N阶行列式计算器
date: 2019-05-07
tags: ["杂项"]
---

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int a[101][101];
    int b[101];

    int main()
    {
        int n,sum=0;
        printf("请输入几阶行列式：");
        scanf("%d",&n);
        for(int i=1;i<=n;i++){
            for(int j=1;j<=n;j++){
                scanf("%d",&a[i][j]);
            }
        }

        for(int i=1;i<=n;i++){
            b[i]=i;
        }
        int ci=1;
        for(int i=1;i<=n;i++){
            ci*=i;
        }
        for(int k=1;k<=ci;k++){
            int flag=0;
            for(int i=1; i<=n; i++){
                for(int j=n;j>=i;j--){
                    if(b[j]>b[i]){
                        flag++;
                    }
                }
            }
            int x=1;
            for(int h=1; h<=n; h++){
                x*=a[h][b[h]];
            }
            if(flag%2){//+
                sum+=x;
            }
            else{//-
                sum-=x;
            }
            next_permutation(b+1,b+1+n);
        }
        printf("%d",sum);
    }

<!-- /wp:code -->