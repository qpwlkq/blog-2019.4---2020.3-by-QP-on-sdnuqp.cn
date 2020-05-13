---
layout: post
title: BF算法
date: 2019-03-29
tags: ["字符串__基础"]
---

<!-- wp:paragraph -->

先看百度词条的描述：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

BF算法，即暴风(Brute Force)算法，是普通的模式匹配算法，BF算法的思想就是将目标串S的第一个字符与模式串T的第一个字符进行匹配，若相等，则继续比较S的第二个字符和 T的第二个字符；若不相等，则比较S的第二个字符和T的第一个字符，依次比较下去，直到得出最后的匹配结果。BF算法是一种蛮力算法。

<!-- /wp:paragraph -->

<!-- wp:code -->

                                      -----------------百度词条

<!-- /wp:code -->

<!-- wp:paragraph -->

只是看看描述，该算法就已清晰，这个算法其实大家都能想到，对于暴力的优化。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

但问题也很明显，如果在很长的一段串中，模式串匹配不成功的部分总在最后一个字符，那样时间复杂度就上去了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

BF算法思路简单明了，但当匹配失败时，主串的指针回溯到i-j+1位置，j回溯到0，这就明显浪费时间精力了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

BF算法最好情况下时间复杂度为O（n+m），最差情况下时间啊复杂度为O（n * m）,不够好！

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    int BF(char S[],char T[],int pos)
    {//c从第pos位开始搜索匹配
        int i=pos,j=0;
        while(S[i+j]!='\0'&&T[j]!='\0'){
            if(S[i+j]==T[j])
                j++;
            else{
                i++;
                j=0;
            }
        }
        if(T[j]=='\0')
            return i+1;
        else
            return -1;
    }

<!-- /wp:code -->