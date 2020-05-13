---
layout: post
title: HDU-1671/POJ-1630-Phone Lists-Trie字典树
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:paragraph -->

这个题是考察字符串前缀的，有串是别的串的前缀就不行，入门级

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code :

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    using namespace std;

    int sum;

    struct node {
        int flag;
        node* next[10];
        node() {
            flag = 0;
            for (int i = 0; i <= 9; ++i) {
                next[i] = NULL;
            }
        }
    };

    node* root;

    void free_node(node* p) {
        for (int i = 0; i <= 9; i++) {
            if (p->next[i] != NULL) {
                free_node(p->next[i]);
            }
        }
        delete p;
    }

    void Insert(char word[]) {
        node* p = root;
        int flag = 1;
        int fl = 0;
        for (int i = 0; word[i]; i++) {
            if (p->next[word[i] - '0'] == NULL) {
                p->next[word[i] - '0'] = new node;
                fl = 1;
            }
            if (p->flag == 1) {
                flag = 0;
            }
            p = p->next[word[i] - '0'];
        }
        if (flag == 0 '' fl == 0)
            sum++;
        p->flag = 1;
    }

    int main() {
        int T;
        int n;
        char word[20];
        scanf("%d", &T);
        while (T--) {
            root = new node;
            sum = 0;
            scanf("%d", &n);
            for (int k = 1; k <= n; k++) {
                scanf("%s", word);
                Insert(word);
            }
            printf(sum == 0 ? "YES\n" : "NO\n");
            free_node(root);
        }

        return 0;
    }

<!-- /wp:code -->