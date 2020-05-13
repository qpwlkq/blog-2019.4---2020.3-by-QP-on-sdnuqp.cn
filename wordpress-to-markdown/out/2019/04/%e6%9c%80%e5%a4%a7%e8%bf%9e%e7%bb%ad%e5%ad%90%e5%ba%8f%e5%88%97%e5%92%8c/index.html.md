---
layout: post
title: 最大连续子序列和
date: 2019-04-02
tags: ["基本策略__动态规划"]
---

<!-- wp:paragraph -->

问题描述：一排数，要你找其中的一段子序列和的最大值。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

最无脑的做法是O(n^2)算法暴力。。。。枚举所有子段，然后计算比较。。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

对于这个问题有很多方法，时间复杂度，空间复杂度 各 有 不 同 。其实，只要会了最简单的O(n)的算法就好了，利用动态规划的思想！

<!-- /wp:paragraph -->

<!-- wp:code -->

    long maxSubSum4(const vector<int>& a) ///复制别人的，就不自己写了
    { 
           long maxSum = 0, thisSum = 0; 
           for (int j = 0; j < a.size(); j++) 
           { 
                  thisSum += a[j]; 
                  if (thisSum > maxSum) 
                         maxSum = thisSum; 
                  else if (thisSum < 0) 
                         thisSum = 0; 
           } 
           return maxSum; 
    } 

<!-- /wp:code -->