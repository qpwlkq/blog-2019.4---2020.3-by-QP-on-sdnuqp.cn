---
layout: post
title: HDU-1247-Hat's word-Trie
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    char word[50010][50];

    struct node {
        int flag;
        node* next[26];
        node() {
            flag = 0;
            for (int i = 0; i <= 25; ++i)
                next[i] = NULL;
        }
    };

    node root;

    void Insert(char *word) {
        node* p = &root;
        for (int i = 0; word[i]; i++) {
            if (p->next[word[i] - 'a'] == NULL)
                p->next[word[i] - 'a'] = new node;
            p = p->next[word[i] - 'a'];
        }
        p->flag = 1;
    }

    int fnd(char *word) {
        int flag = 0;
        node* p = &root;
        for (int i = 0; word[i]; i++) {
            if (p->next[word[i] - 'a'] != NULL)
                p = p->next[word[i] - 'a'];
            else {
                flag = 1;
                break;
            }
        }
        if (p->flag == 0)
            flag = 1;
        return flag ? 0 : 1;
    }

    int main() {
        int cnt = 1;
        while (scanf("%s", word[cnt]) != EOF) {
            Insert(word[cnt++]);
        }
        for (int i = 1; i < cnt; ++i) {
            int len = strlen(word[i]);
            for (int j = 1; j < len; ++j) {
                char wd1[50] = {'\0'};
                char wd2[50] = {'\0'};
                strncpy(wd1, word[i], j);
                strncpy(wd2, word[i] + j, len - j);
                //printf("%s %s\n", wd1, wd2);
                if (fnd(wd1) && fnd(wd2)) {
                    printf("%s\n",word[i]);
                    break;
                }
            }
        }
        return 0;
    }

<!-- /wp:code -->