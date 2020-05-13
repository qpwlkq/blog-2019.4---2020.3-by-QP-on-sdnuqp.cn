---
layout: post
title: [专题一：简单搜索]POJ-3087-Shuffle'm Up-模拟
date: 2019-05-22
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    //#include <bits/stdc++.h>
    using namespace std;

    char s1[110];
    char s2[110];
    char s3[110];
    char s12[220];
    char s21[220];

    int main() {
        int n,t;
        scanf("%d",&t);
        for(int k = 1; k <= t ; k++) {
            scanf("%d",&n);
            getchar();
            scanf("%s",s1);
            getchar();
            scanf("%s",s2);
            getchar();
            scanf("%s",s12);

            strcpy(s3,s1);
            int cnt = 0;
            int is_find = 0;
            while(1) {
                cnt++;
    //            printf("%d>>>>\n",cnt);
    //            printf("%s\n",s1+1);
    //            printf("%s\n",s2+1);
                if(cnt > 1 && strcmp(s1,s3) == 0){
                    break;
                }

                for(int i = 0 ; i < n*2 ; i++) {
                    if(i%2 == 0) {
                        s21[i] = s2[i/2];
                    } else {
                        s21[i] = s1[i/2];
                    }
                }
                s21[n*2] = '\0';
    //            printf("%s\n",s21);
    //            printf("%s\n",s12);
    //            s12[0] = ' ';

    //            printf("%s\n",s21);
    //            printf("%s\n",s12);

                int flag = 1;

                if(strcmp(s21,s12) == 0){
                    ;
                }
                else
                    flag = 0;

                if(flag == 1){
                    is_find = 1;
                    break;
                }

                for(int i = 0 ; i < n*2 ; i++) {
                    if(i < n) {
                        s1[i] = s21[i];
                    } else
                        s2[i-n] = s21[i];
                }
                s1[n] = '\0';
                s2[n] = '\0';
            }

            if(is_find) {
                printf("%d %d\n",k,cnt);
            } else {
                printf("%d -1\n",k);
            }

        }
        return 0;
    }

<!-- /wp:code -->