---
layout: post
title: HDU-5056-Boring count-尺取(滑动窗口)
date: 2019-05-07
tags: ["题解"]
---

<!-- wp:paragraph -->

这个题刚开时毫无头绪，后来才知道这种算法。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题有个漏洞，不同位置截出来的相同子串，算是两个子串。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

其他的没什么了，注意 long long int

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <algorithm>
    using namespace std;

    int N,pre,n,sum,x;
    int a[27];
    char s[100010];

    int main() {
        scanf("%d",&N);
        while(N--) {
            scanf("%s",&s);
            scanf("%d",&n);
            pre = 0;
            long long sum = 0;
            memset(a,0,sizeof(a));
            x = strlen(s);
            for(int i = 0; i < x; i++) {
                a[s[i]-'a']++;
                while(a[s[i]-'a']>n) {
                    a[s[pre]-'a']--;
                    pre++;
                }
                sum += i - pre + 1;
            }
            printf("%lld\n",sum);
        }
        return 0;
    }

<!-- /wp:code -->