---
layout: post
title: POJ-3494-Largest Submatrix of All 1’s-单调栈
date: 2019-07-20
tags: ["数据结构__单调栈","题解"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <algorithm>
    #include <cstring>
    #include <stack>
    //#include <bits/stdc++.h>
    using namespace std;

    int n, m;
    int h[2001];
    int a[2001];
    stack<int>st;

    int main() {
        int z;
        int temp;
        int maxx = 0;
        memset(h,0,sizeof h);
        while(scanf("%d %d", &n, &m)!=EOF) {
            maxx = 0;
            for(int i = 1 ; i <= n ; i++) {
                for(int j = 1; j <= m ; j++) {
                    scanf("%d", &z);
                    if(z == 1) {
                        h[j] = h[j] + 1;
                    } else {
                        h[j] = 0;
                    }
                    a[j] = h[j];
                }
                a[n+1] = -1;
                for(int j = 1; j <= m+1 ; j++) {
                    if(st.empty() '' a[st.top()] <= a[j] ) {
                        st.push(j);
                    } else {
                        while(!st.empty() && a[st.top()] > a[j]) {
                            temp = st.top();
                            maxx = max(maxx, (j - temp) * a[temp]);
                            st.pop();
                        }
                        st.push(temp);
                        a[temp] = a[j];
                    }
                }
            }
            printf("%d\n", maxx);
        }
        return 0;
    }

    /*
    2 2
    0 0
    0 0
    4 4
    0 0 0 0
    0 1 1 0
    0 1 1 0
    0 0 0 0
    */

<!-- /wp:code -->