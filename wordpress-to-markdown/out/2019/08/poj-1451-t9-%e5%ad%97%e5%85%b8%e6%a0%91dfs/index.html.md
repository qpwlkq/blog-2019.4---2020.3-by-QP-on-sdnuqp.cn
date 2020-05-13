---
layout: post
title: POJ-1451-T9-字典树+DFS
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:paragraph -->

漏了两句话：  

More precisely, with every character typed, the phone will show the most probable combination of characters it has found up to that point.  

Let us assume that the phone knows about the words "idea" and "hello", with "idea" occurring more often. Pressing the keys 4, 3, 5, 5, and 6, one after the other,  

the phone offers you "i", "id", then switches to "hel", "hell", and finally shows "hello".

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

两个不同单词，相同前缀的概率是可以相加的，我忘记考虑了O.o

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

新算法：  
 node{  
     int flag;  
     node* next[26];  
 }  
 重新建树，next，26字母，节点flag += m(当前字符串的频率)。  
 每次DFS搜三个next方向,比较前缀频率时，比较的是最后结尾的flag值(与中间字符的flag没关系),然后输出。  
 我没有再去实现，思路肯定是正确的，这题并不难。。。我去找了一篇和我思路相同的代码(好难找O.o)，贴在下面了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

My WA code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <algorithm>
    #include <cstring>
    #include <map>
    using namespace std;

    map<char, int >mp;

    struct node {
        int flag;
        char s[21];
        node* next[10];
        node() {
            flag = 0;
            memset(s, '\0', sizeof s);
            memset(next, NULL, sizeof next);
        }
    };

    node root;

    void Insert(char *word ,int index) {
        node* p = &root;
        for (int i = 0; word[i]; ++i) {
            if (p->next[mp[word[i]]] == NULL)
                p->next[mp[word[i]]] = new node;
            p = p->next[mp[word[i]]];
            if (p->flag <= index) {
                p->flag = index;
                strncpy(p->s, word,i+1);
            }
        }
    }

    void Find(char *w) {
        node* p = &root;
        for (int i = 0; w[i+1]; ++i) {
            p = p->next[w[i] - '0'];
            if (p == NULL) {
                for(int j = i ; w[j+1] ; ++j)
                    printf("MANUALLY\n");
                return;
            }
            printf("%s\n", p->s);
        }
    }

    int main() {
        freopen("input.txt", "r", stdin);
        freopen("output.txt", "w", stdout);
        int T;
        int n, m;
        mp['a'] = mp['b'] = mp['c'] = 2;
        mp['d'] = mp['e'] = mp['f'] = 3;
        mp['g'] = mp['h'] = mp['i'] = 4;
        mp['j'] = mp['k'] = mp['l'] = 5;
        mp['m'] = mp['n'] = mp['o'] = 6;
        mp['p'] = mp['q'] = mp['r'] = mp['s'] = 7;
        mp['t'] = mp['u'] = mp['v'] = 8;
        mp['w'] = mp['x'] = mp['y'] = mp['z'] = 9;

        char word[21];
        scanf("%d",&T);
        for (int i = 1; i <= T; ++i) {
            scanf("%d", &n);
            for (int j = 1; j <= n; ++j) {
                scanf("%s %d", word, &m);
                Insert(word,m);
            }

            scanf("%d", &m);
            printf("Scenario #%d:\n", i);
            for (int j = 1; j <= m; ++j) {
                char w[21] = {'\0'};
                scanf("%s",w);
                Find(w);
                printf("\n");
            }
            printf("\n");
            root = node();
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

链接：https://www.cnblogs.com/183zyz/archive/2011/04/29/2033034.html

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Others AC code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    # include<stdio.h>
    # include<string.h>
    # include<stdlib.h>
    # define PI 110
    # define MAX 26
    struct Trie{
        int num;
        struct Trie *next[MAX];
    };
    int ans,dir[11]={0,0,0,3,6,9,12,15,19,22,26},len,k,max[PI];//记录手机上的每个数字所表示的字母
    char st[PI],map[PI][PI],adj[PI];
    Trie *NewTrie()
    {
        int i;
        Trie *temp= new Trie;
        temp->num=1;
        for(i=0;i<MAX;i++)
            temp->next[i]=NULL;
        return temp;
    }//初始化。。
    void Insert(Trie *p,char s[])
    {
        int i,len1;
        Trie *temp=p;
        len1=strlen(s);
        for(i=0;i<len1;i++)
        {
            if(temp->next[s[i]-'a']==NULL) {temp->next[s[i]-'a']=NewTrie();temp->next[s[i]-'a']->num+=(ans-1);}
            else temp->next[s[i]-'a']->num+=ans;
            temp=temp->next[s[i]-'a'];
        }
    }//插入
    void updata(Trie *p,int step)
    {
        Trie *temp=p;
        int begin,end,j;
            begin=dir[st[step]-'0'];
            end=dir[st[step]-'0'+1];
            for(j=begin;j<end;j++)
            {
                if(temp->next[j]==NULL) continue;
                k++;
                adj[k]=j+'a';
                if(temp->next[j]->num > max[step])
                {
                    max[step] = temp->next[j]->num;
                    adj[k+1]=0;
                    strcpy(map[step],adj);
                }
                if(step!=len-1) updata(temp->next[j],step+1);
                k--;
            }
    }//深搜一遍
    int main()
    {
        Trie *p;
        int i,j,n,m,ncase,t;
        char str[105];
        scanf("%d",&ncase);
        for(t=1;t<=ncase;t++)
        {
            scanf("%d",&n);
            p=NewTrie();
            while(n--)
            {
                scanf("%s %d",str,&ans);
                Insert(p,str);
            }
            scanf("%d",&m);
            printf("Scenario #%d:\n",t);
            while(m--)
            {
                scanf("%s",st);
                len=strlen(st);
                len--;
                k=-1;
                memset(max,-1,sizeof(max));
                updata(p,0);
                for(i=0;i<len;i++)
                {
                    if(max[i]!=-1) printf("%s\n",map[i]);
                    else break;
                }
                for(j=i;j<len;j++)
                    printf("MANUALLY\n");
                printf("\n");
            }
            printf("\n");
        }
        return 0;
    }

<!-- /wp:code -->