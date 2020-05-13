---
layout: post
title: ZOJ-1109-Language of FatMouse-Trie字典树
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:paragraph -->

注意node节点存的什么，要灵活变化！

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    struct node {
        int flag;
        char s[11];
        node* next[26];
        node() {
            flag = 0;
            for (int i = 0; i <= 25; i++)
                next[i] = NULL;
        }
    };

    node root;

    void Insert(char *word, char *sf) {
        node* p = &root;
        for (int i = 0; word[i] ; ++i) {
            if (p->next[word[i] - 'a'] == NULL)
                p->next[word[i] - 'a'] = new node;
            p = p->next[word[i] - 'a'];
        }
        p->flag = 1;
        strcpy(p->s, sf);
    }

    int fnd(char* word) {
        int flag = 1;
        node* p = &root;
        for (int i = 0; word[i]; ++i) {
            if (p->next[word[i] - 'a'] != NULL)
                p = p->next[word[i] - 'a'];
            else {
                flag = 0;
                break;
            }
        }
        if (p->flag == 0) {
            return 0;
        }
        if (flag == 1) {
            printf("%s\n", p->s);
            return 1;
        }
        return 0;
    }

    int main() {
        char wd1[11], wd2[11];
        while (scanf("%s", wd1) != EOF) {
            if (getchar() == '\n') {
                if (fnd(wd1) == 0)
                    printf("eh\n");
                break;
            }
            scanf("%s", wd2);
            Insert(wd2,wd1); 
        }
        while (scanf("%s", wd1) != EOF) {
            if (fnd(wd1) == 0)
                printf("eh\n");
        }
    }

<!-- /wp:code -->