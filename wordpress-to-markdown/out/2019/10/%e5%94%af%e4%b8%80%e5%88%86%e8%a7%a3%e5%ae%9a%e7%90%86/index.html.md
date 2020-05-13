---
layout: post
title: 唯一分解定理
date: 2019-10-06
tags: ["数论___唯一分解定理"]
---

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">唯一分解定理（算术基本定理）
 证明：反证法，详见百度百科
 1.一个大于1的整数n，唯一分解式：n = p1^a1 * p2^a2 _..._pn^an
 2.正因数个数：sum = (1+a1)(1+a2)...(1+an)
 3.正因数之和：ans = (1 + p1^1 + p1^2 +...+ p1^a1)(1 + p2^1 +...+p2^a2)...(1 + pn^1 +...+ pn^an)
 4.gcd(a,b)_lcm(a,b) = a_b;(反用时，注意a*b是否会溢出！)

 code:

 #include <bits/stdc++.h> 
 using namespace std;
 int n;
 int a[1010];
 int vis[1010];
 int main(){
     int n;
     scanf("%d",&n);
     int cnt = 0;
     for(int i = 2 ; i <= n ; i++){
         if(n%i == 0)
             vis[cnt] = i;
         while(n%i == 0){
             a[cnt]++;
         }
         cnt++;
     }
     for(int i = 0 ; i < cnt-1 ; i++){
         printf("%d^%d * ",vis[i],a[i]);
     }
     printf("%d^%d\n",vis[i],a[i]);
     return 0;
 }</pre>
<!-- /wp:preformatted -->