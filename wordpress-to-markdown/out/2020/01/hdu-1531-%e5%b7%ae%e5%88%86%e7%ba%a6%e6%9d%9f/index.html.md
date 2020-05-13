---
layout: post
title: HDU-1531-差分约束
date: 2020-01-31
tags: ["基础__STL"]
---

<!-- wp:paragraph -->

做到hdu1364时搜题解, 第一篇题解竟然是个假的, 套着羊皮的狼, 作者标错题号了,顺便看看.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

题目很有意思, 但是.............显然不会, 滑稽.

<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">差分约束:  如果一个系统由n个变量和m个约束条件组成，形成m个形如ai-aj≤k的不等式(i,j∈[1,n],k为常数),则称其为差分约束系统(system of difference constraints)。亦即，差分约束系统是求解关于一组变量的特殊不等式组的方法。</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->

求解差分约束系统，可以转化成图论的单源最短路径（或最长路径）问题。 观察xj-xi<=bk，会发现它类似最短路中的三角不等式d[v]<=d[u]+w[u,v]，即d[v]-d[u]<=w[u,v] [1]  。因此，以每个变量xi为结点，对于约束条件xj-xi<=bk，连接一条边(i,j)，边权为bk。我们再增加一个源点s,s与所有定点相连，边权均为0。对这个图，以s为源点运行Bellman-ford算法（或SPFA算法），最终{d[i]}即为一组可行解。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

                                                                                                             -------百度词条

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

总之, 建图最重要.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[https://www.cnblogs.com/liyinggang/p/5697436.html](https://www.cnblogs.com/liyinggang/p/5697436.html)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

大佬的code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <cstdio>
    #include <iostream>
    #include <algorithm>
    using namespace std;
    int lim;
    int mp[150][150];
    int n, m;
    int lr[100017][2];
    char ch[100017];
    int ok(int x, int y){
        if (x <= n && x >= 1 && y >= 1 && y <= m){
            if (mp[x][y] == 0)
                return 1;
        }
        return 0;
    }

    int dfs(int x, int y, int nw){
        if (!ok(x, y))
            return 0;
        if (nw == lim)
            return 1;
        if (ch[nw] == 'R'){
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x, y + i))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x, y + i))
                    break;
                if (dfs(x, y + i, nw + 1))
                    return 1;
            }
        }
        if (ch[nw] == 'L'){
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x, y - i))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x, y - i))
                    break;
                if (dfs(x, y - i, nw + 1))
                    return 1;
            }
        }
        if (ch[nw] == 'U'){
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x - i, y))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x - i, y))
                    break;
                if (dfs(x - i, y, nw + 1))
                    return 1;
            }
        }
        if (ch[nw] == 'D')
        {
            for (int i = 1; i < lr[nw][0]; i++){
                if (!ok(x + i, y))
                    return 0;
            }
            for (int i = lr[nw][0]; i <= lr[nw][1]; i++){
                if (!ok(x + i, y))
                    break;
                if (dfs(x + i, y, nw + 1))
                    return 1;
            }
        }
        return 0;
    }

    int main(){
        int t;
        scanf("%d", &t);
        while (t--){
            scanf("%d%d", &n, &m);
            for (int i = 1; i <= n; i++)
                for (int j = 1; j <= m; j++)
                    scanf("%d", &mp[i][j]);
            int l, r;
            lim = 0;
            char c;
            while (scanf("%d%d", &l, &r), l '' r){
                getchar();
                cin >> c;
                if (l > r)
                    swap(l, r);
                lr[lim][0] = l;
                lr[lim][1] = r;
                ch[lim++] = c;
            }
            int ans = 0;
            for (int ii = 1; ii <= n; ii++){
                for (int j = 1; j <= m; j++){
                    if (ok(ii, j) && dfs(ii, j, 0))
                        ans++;
                }
            }
            printf("%d\n", ans);
        }
        return 0;
    }

<!-- /wp:code -->