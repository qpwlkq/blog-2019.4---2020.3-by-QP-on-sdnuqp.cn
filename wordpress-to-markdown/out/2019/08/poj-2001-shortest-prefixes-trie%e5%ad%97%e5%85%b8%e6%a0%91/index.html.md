---
layout: post
title: POJ-2001-Shortest Prefixes-Trie字典树
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:paragraph -->

这个题比较复杂，我竟然1遍过了，嘿嘿黑。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题是要你找很多字符串的缩写，规则是

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

1.最短。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

2.该子串没有歧义（不是其他串的子串）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

我的思路是，建树时，每个节点记录走过的次数。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

最后去查找的时候，查到第一个flag值 == 1 的点，说明只有1个串经过这个节点，当然这就是该串的最短前缀了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

OVER

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;

    char word[1001][21];

    struct node {
        int num;
        node* next[26];
        node() {
            num = 0;
            memset(next, NULL, sizeof next);
        }
    };

    node root;

    void Insert(char* word) {
        node* p = &root;
        for (int i = 0; word[i]; ++i) {
            if (p->next[word[i] - 'a'] == NULL)
                p->next[word[i] - 'a'] = new node;
            p = p->next[word[i] - 'a'];
            p->num++;
        }
    }

    void Find(char *word) {
        node* p = &root;
        for (int i = 0; word[i]; ++i) {
            p = p->next[word[i] - 'a'];
            printf("%c",word[i]);
            if (p->num == 1) {
                printf("\n");
                return;
            }
        }
        printf("\n");
    }

    int main() {
        int cnt = 1;
        while (scanf("%s", word[cnt]) != EOF) {
            Insert(word[cnt++]);
        }
        for (int i = 1; i < cnt; i++) {
            printf("%s ",word[i]);
            Find(word[i]);
        }
        return 0;
    }

<!-- /wp:code -->