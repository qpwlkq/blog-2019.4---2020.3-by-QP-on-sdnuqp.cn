---
layout: post
title: 子集生成算法
date: 2019-07-26
tags: ["算法"]
---

<!-- wp:paragraph -->

1.增量构造法，递推，DFS

<!-- /wp:paragraph -->

<!-- wp:code -->

    /*

     子集生成算法
     1.增量构造法
     2.位向量法
     3.二进制法

    */

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 100 + 1;

    int n;
    int A[maxn];

    void print_subset(int n , int * A, int cur) {
        for (int i = 0; i < cur; i++) {
            printf("%d ", A[i]);
        }
        printf("\n");
        int s = cur ? A[cur - 1] + 1 : 0;
        for (int i = s; i < n; i++) {
            A[cur] = i;
            print_subset(n, A, cur + 1);
        }
    }

    int main() {
        scanf("%d", &n);

        print_subset(n, A, 0);
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

2.位向量法 （递推，深搜）

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 100 + 1;

    int n;
    int A[maxn];

    void print_subset(int n , int * A, int cur) {
        if (cur == n) {
            for (int i = 0; i < cur; i++) {
                if (A[i]) printf("%d ", i);
            }
            printf("\n");
            return;
        }
        A[cur] = 1;
        print_subset(n, A, cur + 1);
        A[cur] = 0;
        print_subset(n, A, cur + 1);
    }

    int main() {
        scanf("%d", &n);
        print_subset(n, A, 0);
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

3.二进制法

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;
    const int maxn = 100 + 1;

    int n;
    int A[maxn];

    void print_subset(int n ,int s) {
        for (int i = 0; i < n; i++) {
            if (s & (1 << i)) printf("%d ",i);
        }
        printf("\n");
    }

    int main() {
        scanf("%d", &n);
        for (int i = 1; i < (1 << n); i++) {
            print_subset(n, i);
        }
        return 0;
    }

<!-- /wp:code -->