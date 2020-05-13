---
layout: post
title: 最短路总结
date: 2019-05-09
tags: ["算法"]
---

<!-- wp:paragraph -->

传送门还没写好。。。

<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">主要有3种{  
     1.Dijkstra  
     2.Frody  
     3.Bellman-Ford  
 }及其优化。  
 1 - 迪杰斯特拉算法(Dijkstra){  
     1.1 邻接矩阵/临界表{  
         ......  
     }  
     1.2 优先队列{  
         ......  
     }  
     1.3 二叉堆优化{  
         ......  
     }  
 }  
 2 - 弗洛伊德算法(Flody){  
     ......  
 }  
 2.2 按情况适当优化(从别人的博客摘的){  
     1.跳过不存在的路径  
     2.只用矩阵下三角  
     3.利用矩阵对称性  
     4.避免循环中大量调用函数。  
 }  
 3 - 贝尔曼-福特算法(Bellman-Ford){  
     3.1 基础算法{  
         ......  
     }  
     3.2 队列优化，又名SPFA{  
         3.2.1 SLF(Small Label First)，双端队列优化{  
             ......  
         }  
         3.2.2 LLL(Large Label Last){  
             ......  
        }      
     }  
 }</pre>
<!-- /wp:preformatted -->