---
layout: post
title: [题解]ZOJ-3768-Continuous Login-二分
date: 2019-04-24
tags: ["题解"]
---

<!-- wp:paragraph -->

这个题完全没找到规律，搜了一篇题解，说枚举前20个数，发现一个数最多分成三个数，然后暴力二分。。。  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

 我以为是个递归，我规律找错了。。看了这个，就很好做了，很水嘛O。O，没看别人的code，自己写了一个程序，一遍了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code :

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 123456789;

    int a[16000];

    int one(int x,int maxx) {
        for(int i = 1 ; i <= maxx ; i++) {
            if(a[i] == x) {
                printf("%d\n",i);
                return 1;
            }
        }
        return 0;
    }

    int two(int x, int maxx) {
        int l,mid,r;
        for(int i = 1 ; i <= maxx ; i++) {
            l = i;
            r = maxx;
            mid = (l + r)/2;
            while(l < r) {
                if(a[mid] > x - a[i]) {
                    r = mid ;
                    mid = (l + r)/2;
                } else if(a[mid] < x - a[i]) {
                    l = mid;
                    mid = (l + r)/2;
                } else {
                    printf("%d %d",i,mid);
                    return 1;
                }
                if(r - l == 1) {
                    mid = (r+l)/2;
                    if(a[mid] == x - a[i]) {
                        printf("%d %d",i,mid);
                        return 1;
                    }
                    break;
                }
            }
        }
        return 0;
    }
    int three(int x,int maxx) {
        for(int i = 1 ; i <= maxx ; i++) {
            if(two(x-a[i],maxx)) {
                printf(" %d\n",i);
                return 0;
            }
        }
        return 1;
    }

    int main() {
        int i;
        a[1] = 1;
        for(i = 2 ;; i++) {
            a[i] = a[i-1]+i;
            if(a[i] >= maxn)
                break;
        }
        i-- ;
        int t;
        scanf("%d",&t);
        int z;
        while(t--) {
            scanf("%d",&z);
            if(one(z,i)) {
    //            cout<<"(1)"<<'\n';
                ;
            } else if(two(z,i)) {
                printf("\n");
    //            cout<<"(2)"<<'\n';
                ;
            } else {
    //            cout<<"(3)"<<'\n';
                three(z,i);
            }
        }
        return 0;
    }

    ////OK;

<!-- /wp:code -->