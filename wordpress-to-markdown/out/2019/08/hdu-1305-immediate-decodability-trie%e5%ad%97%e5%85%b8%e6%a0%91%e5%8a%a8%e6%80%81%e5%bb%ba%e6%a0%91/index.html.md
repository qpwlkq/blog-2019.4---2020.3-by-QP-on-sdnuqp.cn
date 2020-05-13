---
layout: post
title: HDU-1305-Immediate Decodability-Trie字典树动态建树
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:paragraph -->

入门级题目，这个题和POJ-1056是一摸一样的，but，测试样例却不一样，这个题你只能动态建树，不然会MLE，而那个题你只能静态建树，不然会TLE！！！！！注意！！！（对有的题来说,不删除指针也会TLE，虽然这个不会，但我懒。大部分时候都不写。。O.o）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code :

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    using namespace std;

    int fl;

    struct Trie {
        int flag;
        Trie* next[2];
        Trie() {
            flag = 0;
            next[0] = next[1] = NULL;
        }
    };

    Trie* root = new Trie;

    void Insert(char word[]) {
        Trie * p = root;
        for (int i = 0; word[i]; i++) {
            if (p->next[word[i] - '0'] == NULL)
                p->next[word[i] - '0'] = new Trie;
            if (p->flag == 1) {
                fl = 1;
            }
            p = p->next[word[i] - '0'];
        }
        p->flag = 1;
    }

    int main() {
        char word[20];
        int cnt = 1;
        while (scanf("%s", word) != EOF) {
            if(word[0] == '9') {
                root->next[0] = root->next[1] = NULL;
                root->flag = 0;
                printf("Set %d is", cnt);
                printf(fl ? " not " : " ");
                printf("immediately decodable\n");
                cnt++;
                fl = 0;
                continue;
            }
            Insert(word);
        }
        return 0;
    }

<!-- /wp:code -->