---
layout: post
title: HDU-2072-Trie字典树判重复串
date: 2019-08-05
tags: ["字符串__Trie字典树"]
---

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <cstring>
    #include <sstream>
    using namespace std;

    int sum;

    struct Trie {
        int flag; ///标记结尾
        Trie* next[26];
        Trie() {
            for (int i = 0; i <= 25; i++) next[i] = NULL;
            flag = 0;
        }
    };

    char word[1010];
    Trie * root;

    void Insert(string word) {
        Trie* p = root;
        int flag = 1;
        for (int i = 0; word[i]; i++) {
            if (p->next[word[i] - 'a'] == NULL) {
                p->next[word[i] - 'a'] = new Trie;
            }
            p = p->next[word[i] - 'a'];
        }
        p->flag++;
        if (p->flag == 1)
            sum++;
    }

    int main() {
        string str, str1;
        while (getline(cin, str))
        {
            root = new Trie();
            sum = 0;
            if (str == "#")
                break;
            istringstream ss(str);
            while (ss >> str1)
            {
                Insert(str1);
            }
            cout << sum << endl;
        }
        return 0;
    }

<!-- /wp:code -->