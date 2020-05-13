---
layout: post
title: SDNUOJ-1118-单词统计-AC自动机
date: 2019-08-17
tags: ["字符串__AC自动机"]
---

<!-- wp:paragraph -->

呵呵,这道题要统计每一个单词的出现次数.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

注意,字符串可能会有重复!!!!!我想了好久,最后才意识到可能只是这错了,我觉得根据题意不应该会有重复串的,可惜题就是题而已,不会考虑真实情况,改了之后,AC.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这题师哥写: 也可以java水过...

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

于是:

<!-- /wp:paragraph -->

<!-- wp:image {"id":524} -->
<figure class="wp-block-image">![](image-1024x496.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->

我笑了.....

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

呵

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

呵呵

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

请看正确题解:

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    map<int, int>mp;

    struct Trie {
        int next[1000010][26], fail[1000010], end[1000010];
        int root, L;
        int newnode() {
            for (int i = 0; i <= 25; i++)
                next[L][i] = -1;
            end[L++] = -1;
            return L - 1;
        }
        void init() {
            memset(num, 0, sizeof num);
            L = 0;
            root = newnode();
        }

        void insert(char word[] ,int cnt) {
            int len = strlen(word);
            int now = root;
            for (int i = 0; i < len; i++) {
                if (next[now][word[i] - 'a'] == -1)
                    next[now][word[i] - 'a'] = newnode();
                now = next[now][word[i] - 'a'];
            }
            end[now] = cnt;
            mp[cnt] = now;
        }

        void build() {
            queue<int>q;
            fail[root] = root;
            for (int i = 0; i <= 25; ++i) {
                if (next[root][i] == -1)
                    next[root][i] = root;
                else {
                    fail[next[root][i]] = root;
                    q.push(next[root][i]);
                }
            }
            while (!q.empty()) {
                int now = q.front();
                q.pop();
                for (int i = 0; i <= 25; ++i) {
                    if (next[now][i] == -1) {
                        next[now][i] = next[fail[now]][i];    ///应用fail，转到其他串上
                    }
                    else {
                        fail[next[now][i]] = next[fail[now]][i]; ///填充fail数组.
                        q.push(next[now][i]);
                    }
                }
            }
        }
        int num[50010];
        void query(char word[]) {
            int len = strlen(word);
            int now = root;
            for (int i = 0; i < len; i++) {
                now = next[now][word[i] - 'a'];
                int temp = now;
                while (temp != root) {
                    //printf("%d\n",end[temp]);
                    if (end[temp] != -1)
                        num[end[temp]]++;
                    //end[temp] = 0;
                    temp = fail[temp];
                }
            }
        }
        void print(int n) {
            printf("%d",num[end[mp[1]]]);
            for (int i = 2; i <= n; i++) {
                printf(" %d", num[end[mp[i]]]);
            }
            printf("\n");
        }
    };

    char word[1000010];
    Trie ac;

    int main() {
        int n;
        while (scanf("%d", &n) != EOF) {

            ac.init();
            for (int i = 1; i <= n; ++i) {
                scanf("%s", word);
                ac.insert(word , i);
            }
            ac.build();
            scanf("%s", word);
            ac.query(word);
            ac.print(n);
        }
        return 0;
    }

    /*

    6
    she
    she
    he
    say
    shr
    her
    sheyasherhs
    5
    she
    he
    say
    shr
    her
    yasherhs
    7
    a
    ab
    ba
    aba
    aba
    bab
    bab
    aababa

    */

<!-- /wp:code -->