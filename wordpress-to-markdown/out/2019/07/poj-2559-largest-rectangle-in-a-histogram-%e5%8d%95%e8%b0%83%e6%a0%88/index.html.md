---
layout: post
title: POJ-2559-Largest Rectangle in a Histogram-单调栈
date: 2019-07-20
tags: ["数据结构__单调栈","题解"]
---

<!-- wp:code -->

    #include <iostream>
    #include <cstdio>
    #include <algorithm>
    #include <cstring>
    #include <stack>
    using namespace std;
    typedef long long ll;

    ll n;
    struct node {
        ll x;
        ll sum;
    };

    stack <node> st;

    int main() {
        node q;
        ll z;
        ll temp;
        ll S;
        ll maxx;
        while(scanf("%I64d", &n) != EOF && n ) {
            maxx = 0;
            for(int i = 1; i <= n ; i ++) {
                scanf("%I64d", &q.x);
                q.sum = 1;
                temp = 0;
                if(st.empty()) {
                    st.push(q);
                } else if(st.top().x >= q.x){
                    while(!st.empty() && (st.top()).x >= q.x) {
                        (st.top()).sum += temp;
                        S = (st.top()).x * (st.top()).sum;
                        maxx = max(maxx, S);
                        temp = (st.top()).sum;
                        st.pop();
                    }
                    q.sum += temp;
                    st.push(q);
                }
                else{
                    st.push(q);
                }
            }
            temp = 0;
            while(!st.empty()) {
               (st.top()).sum += temp;
                S = (st.top()).sum * (st.top()).x ;
                maxx = max(maxx, S);
                temp = (st.top()).sum;
                st.pop();
            }
            printf("%I64d\n",maxx);
        }
        return 0;
    }

<!-- /wp:code -->