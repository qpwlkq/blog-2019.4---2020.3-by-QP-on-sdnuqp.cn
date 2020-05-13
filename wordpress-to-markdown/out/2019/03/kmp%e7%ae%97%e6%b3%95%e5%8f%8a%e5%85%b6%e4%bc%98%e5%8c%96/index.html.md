---
layout: post
title: KMP算法及其优化
date: 2019-03-29
tags: ["字符串__KMP/EXKMP","字符串__基础"]
---

<!-- wp:paragraph -->

如约而至

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

首先，我建议你别看我的博客了，。。。。。。因为有人个写的比我强10000倍。。。。Orz。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[某大神写的KMP详解，写的太好了啊啊啊啊，点我传送，起飞。。](https://blog.csdn.net/x__1998/article/details/79951598)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

好了，你非要看我的我也没办法，嗯~ o(_￣▽￣_)o，我讲的乱七八糟，主要给自己看的，请点赞。。。

<!-- /wp:paragraph -->

<!-- wp:heading -->

## 1- 1 基础KMP算法

<!-- /wp:heading -->

<!-- wp:paragraph -->

KMP算法是一种改进的字符串匹配算法，由D.E.Knuth，J.H.Morris和V.R.Pratt同时发现，因此人们称它为克努特--莫里斯--普拉特操作（简称KMP算法）。KMP算法的关键是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。具体实现就是实现一个next()函数，函数本身包含了模式串的局部匹配信息。时间复杂度O(m+n)。

<!-- /wp:paragraph -->

<!-- wp:code -->

    -------百度百科

<!-- /wp:code -->

<!-- wp:paragraph -->

反正KMP就是三个人的名字缩写，KMP算法是一种改进能够快速的进行字符串匹配的算法。嗯~ o(_￣▽￣_)o。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

先上模板，代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    int KMP(char * t, char * p) 
    {
        int i = 0; 
        int j = 0;

        while (i < strlen(t) && j < strlen(p))
        {
            if (j == -1 '' t[i] == p[j]) 
            {
                i++;
                j++;
            }
            else 
                j = next[j];
            }

        if (j == strlen(p))
           return i - j;
        else 
           return -1;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

得到next数组，代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    void getNext(char * p, int * next)
    {
        next[0] = -1;
        int i = 0, j = -1;

        while (i < strlen(p))
        {
            if (j == -1 '' p[i] == p[j])
            {
                ++i;
                ++j;
                next[i] = j;
            }   
            else
                j = next[j];
        }
    }

<!-- /wp:code -->

<!-- wp:heading {"level":3} -->

### 以模式串"abababcccab"为例

<!-- /wp:heading -->

<!-- wp:paragraph -->

**next数组作用：记录在第i个字符匹配失败的时候，j应该回溯到哪个位置！**

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

next[]数组是存"模式串的子串中相同的前缀和后缀最大长度"，子串长度为1时，没有前缀后缀，next[1]=0

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

next[2],即子串是"ab"时,相同前缀后缀最大长度，前缀只有"a",后缀只有"b",不相等，所以next[2]=0

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

next[3]，即子串是"aba"时,前缀两个"a"和"ab",后缀两个"a"和"ba",都有"a",长度1，所以next[3]=1，到这就明白next数组的意义了吧，但关键是如何用代码得到？

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

（还有一种优化算法，使用newnext数组，后面再说。）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

噫- - - -，有没有发现上面两个函数貌似一样啊？

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

没错就是一样的！！！只不过第二个求next的函数中两个串是一样的，都是模式串，第一个KMP函数中一个主串，一个子串，。。。Orz.......

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

刚开始没好好看这篇博客，没理解，又去找了一堆视频博客，也没搞懂，反而自己混乱了，省略一系列过程，最终又点开了开头链接的那篇博客，往下翻了翻，看到那几张得到next数组的过程图，卧槽，窝里个去，我擦力，恍然啊东大坞！！！

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

白浪费那么多时间了。。。。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### KMP到这为止了，next数组得出请看：

<!-- /wp:heading -->

<!-- wp:paragraph -->

**_推荐博客的几张过程图！_**

<!-- /wp:paragraph -->

<!-- wp:heading -->

## 1- 2 KMP算法的优化

<!-- /wp:heading -->

<!-- wp:paragraph -->

又回来了，本以为对这个算法已经理解透了，代码也会了，做了一个题，结果还是有几个样例TLE了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

P3375题，最开始介绍的算法超时（主要就是next数组中的值还可以优化），我一看题解，大多数人都用的另一种for循环中套while的方法。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

        int j=0;
        for (int i=2; i<=lb; i++) {
            while(j&&b[i]!=b[j+1])
                j=kmp[j];
            if(b[j+1]==b[i])
                j++;
            kmp[i]=j;
        }
        for(int i=1; i<=la; i++) {
            while(j&&b[j+1]!=a[i])
                j=kmp[j];
            if (b[j+1]==a[i])
                j++;
            if (j==lb) {
                cout<<i-lb+1<<endl;
                j=kmp[j];
            }
        }

<!-- /wp:code -->

<!-- wp:paragraph -->

[链接](https://blog.csdn.net/u012852986/article/details/51413305)

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 另，另一种优化方法

<!-- /wp:heading -->

<!-- wp:paragraph -->

使用nextval数组，这个是数据结构课本上的优化，旨在防止这种情况：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

aaaaaaaaaaaaab（T串）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

aaaab(P串)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

一旦发现一堆a相同，直接跳到结尾，不用一位位的挪了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    void getNextval(){
        nextval[1] = 0;
        i = 1;
        j = 0;
        while(i<len2){
            if( j==0 '' m[i] == m[j]){
                i++;
                j++;
                if(m[i] != m[j]){
                    nextval[i] = j;
                }
                else{
                    nextval[i] = nextval[j];
                }
            }
            else{
                j = nextval[j];
            }
        }
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

数据结构课本上的内容。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

补写一些东西

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

时隔半年之后，再回来看KMP，发现自己还是不会。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

一直挂在心上，对KMP的理解实在不够！趁着暑假集训，重启KMP，此次必须精通！

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

2019.8.6

<!-- /wp:paragraph -->