---
layout: post
title: foreach?
date: 2019-04-30
tags: ["杂项"]
---

<!-- wp:paragraph -->

今天学java时学到了一个叫foreach的东西，突然想起来C++中也有类似的结构，很好用，但我没用过。。。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int x,y;

    int main(){
        int z[6] = {0,1,2,3};
        for(int i : z){
            printf("%d ",z[i]);
        }
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

stl容器迭代和数组都可以用。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

输出：0，1，2，3，0，0.

<!-- /wp:paragraph -->