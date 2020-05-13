---
layout: post
title: HDU-1251-统计难题-Trie查前缀
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:paragraph -->

经典入门题

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC node:

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