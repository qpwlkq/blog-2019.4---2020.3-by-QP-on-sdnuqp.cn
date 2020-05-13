---
layout: post
title: [专题二：搜索进阶]HDU-3533-Escape-BFS+预处理
date: 2019-05-28
tags: ["kuangbin专题","题解"]
---

<!-- wp:paragraph -->

这个题真的把我做崩了。删删减减至少写了1000行。。。。中间打表的部分死活做不对（做了几乎整整一晚上。。。），最后借鉴了一位大神的博客，Orz，我写废了的也跟在后面了。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #pragma GCC optimize(2)

    #include <cstdio>
    #include <algorithm>
    #include <cstring>
    #include <queue>
    using namespace std;
    const int maxn = 100 + 2;

    struct node {
        int x;
        int y;
        int sum;///能量
    };

    struct p {
        char chr;
        int t,v,x,y;
    } store_fortress[101];

    bool mark_fortress[maxn][maxn];
    bool mark_map[maxn][maxn][1002];
    bool mark_bullet[1002][maxn][maxn];

    int m,n,k,d;
    char dir;
    int t,v,x,y;
    int ds[5][2] = {{0,0},{1,0},{0,1},{-1,0},{0,-1}};

    void treaval() {
        for(int t = 1; t <= d ; t++) {
            printf("%d>>>\n",t);
            for(int i = 0 ; i <=  m ; i++) {
                for(int j = 0 ; j <= n ; j++) {
                    printf("%d ",mark_bullet[t][i][j]);
                }
                printf("\n");
            }
            printf(">>>>>>>>>\n");
        }
    }

    void update(char id, int t,int v, int x,int y) {

        if(id == 'W') {
            int stop = 0;
    //        for(int j = y - 1; j >= 0; j --) {
    //            if(mark_fortress[x][j]) {
    //                stop = j;
    //                break;
    //            }
    //        }
            for(int j = y - v,ini = 1; j >= 0; j -= v,ini ++) {
                for(int k = ini; k <= d; k += t) {
                    mark_bullet[k][x][j] = true;
                }
                if(mark_fortress[x][j]){
                    break;
                }
            }

        } else if(id == 'E') {
            for(int j = y + v,ini = 1; j <= m; j += v,ini ++) {
                for(int k = ini; k <= d; k += t) {
                    mark_bullet[k][x][j] = true;
                }
                if(mark_fortress[x][j]) {
                    break;
                }
            }
        } else if(id == 'N') {
            for(int j = x - v,ini = 1; j >= 0; j -= v,ini ++) {
                for(int k = ini; k <= d; k += t) {
                    mark_bullet[k][j][y] = true;
                }
                if(mark_fortress[j][y]) {
                    break;
                }
            }
        } else if(id == 'S') {
            for(int j = x + v,ini = 1; j <= n; j += v,ini ++) {
                for(int k = ini; k <= d; k += t) {
                    mark_bullet[k][j][y] = true;
                }
                if(mark_fortress[j][y]) {
                    break;
                }
            }
        }
    }

    inline bool check(int x,int y,int t) {

        if(mark_map[x][y][t] == 0 && mark_bullet[t][x][y] == 0 && mark_fortress[x][y] == 0 && x >= 0 && y >= 0 && x <= m && y <= n)
            return 1;
        return 0;
    }

    queue<node>q;
    void bfs() {
        node p,t;
        p.x = 0 ;
        p.y = 0;
        p.sum = 0;
        q.push(p);
        mark_map[0][0][0] = 1;
        while(!q.empty()) {
            p = q.front();
            q.pop();
            if(p.x == m && p.y == n) {
                printf("%d\n",p.sum);
                while(!q.empty()) {
                    q.pop();
                }
                return ;
            }
            if(p.sum > d)
                continue;
            for(int i = 0 ; i <= 2 ; i++) {
                t.x = p.x + ds[i][0];
                t.y = p.y + ds[i][1];
                t.sum = p.sum + 1;
                if(check(t.x, t.y, t.sum)) {
                    mark_map[t.x][t.y][t.sum] = 1;
                    q.push(t);
                }
            }
        }
        printf("Bad luck!\n");
        return ;
    }
    int main() {

        while(scanf("%d %d %d %d",&m,&n,&k,&d) != EOF) {
            getchar();
            memset(mark_fortress,0,sizeof mark_fortress);
            memset(mark_map,0,sizeof mark_map);
            memset(mark_bullet,0,sizeof mark_bullet);

    //        fill(&mark_fortress[0][0],&mark_fortress[maxn-1][maxn-1],false);
    //        fill(&mark_bullet[0][0][0],&mark_bullet[1001][maxn-1][maxn-1],false);
    //        fill(&mark_map[0][0][0],&mark_map[maxn][maxn-1][1001],false);

            for(int i = 1 ; i <= k ; i++) {
                scanf("%c %d %d %d %d",&store_fortress[i].chr,&store_fortress[i].t,&store_fortress[i].v,&store_fortress[i].x,&store_fortress[i].y);
                getchar();
                mark_fortress[store_fortress[i].x][store_fortress[i].y] = 1;
            }

            for(int i = 1; i <= k ; i++) {
                update(store_fortress[i].chr,store_fortress[i].t,store_fortress[i].v,store_fortress[i].x,store_fortress[i].y);
            }

            bfs();

    //        treaval();

        }
        return 0;
    }

    /*
    4 4 3 10
    N 1 1 1 1
    W 1 1 3 2
    W 1 1 2 4
    8

    4 4 3 10
    N 1 1 1 1
    W 1 1 3 2
    W 2 1 2 4
    4 4 3 10
    N 1 1 1 1
    W 1 1 3 2
    W 1 1 2 4

    */

    /*
    W3
    E4
    N1
    S2
    N
    S
    W
    E

    */

    /*
    void update(int a[][5]) {
        for(int t = 1; t <= d ; t++) {///时间轴
            for(int i = 1; i <= k ; i++) {
                int id = a[i][0];///方向
                int cycle = a[i][1];///周期
                int one_dis = a[i][2];///速度
                int num_bullet = (t-1)/cycle+1;///子弹个数
                int len = t*one_dis;   ///最远的子弹离堡垒的距离
                int x = a[i][3];
                int y = a[i][4];

                if(id == 1) {      ///N
    //                if(num_bullet * one_dis > x) {
    //                    continue;
    //                }
    //                printf("1\n");
                    for(int j = x-1 ; j >= 0 ; j--) {
                        if(mark_fortress[j][y] == 1) {
                            break;
                        }
                        if(num_bullet) {
                            if((x-j)%one_dis != 0)
                                continue;
                            num_bullet--;
                            mark_bullet[t][j][y] = 1;
                        } else {
                            break;
                        }
                    }
                } else if(id == 2) { ///S
    //                printf("2\n");
    //                if(num_bullet * one_dis > m - x) {
    //                    continue;
    //                }
                    for(int j = x+1 ; j <= m ; j++) {
                        if(mark_fortress[j][y] == 1) {
                            break;
                        }
                        if(num_bullet) {
                            if((j-x)%one_dis != 0)
                                continue;
                            num_bullet--;
                            mark_bullet[t][j][y] = 1;
                        } else {
                            break;
                        }
                    }
                } else if(id == 3) { ///W
    //                printf("3\n");
    //                if(num_bullet * one_dis > y) {
    //                    continue;
    //                }
                    if(t%cycle != 0) {
                        for(int j = y - 1 ; j >= 0 ; j--) {
                            if(mark_fortress[x][j] == 1) {
                                break;
                            }
                            if(a[j] == 1) {
                                a[j] ==
                            }
                        }
                    }
                    for(int j = y-1 ; j >= 0 ; j--) {
                        if(mark_fortress[x][j] == 1) {
                            break;
                        }
                        if(num_bullet) {
                            num_bullet--;
                            mark_bullet[t][x][j] = 1;
                        } else {
                            break;
                        }
                    }
                } else if(id == 4) { ///E
    //                printf("4\n");
    //                if(num_bullet * one_dis > n - y) {
    //                    continue;
    //                }
                    for(int j = y+1 ; j <= n ; j++) {
                        if(mark_fortress[x][j] == 1) {
                            break;
                        }
                        if(num_bullet) {
                            if((j-y)%one_dis != 0)
                                continue;
                            num_bullet--;
                            mark_bullet[t][x][j] = 1;
                        } else {
                            break;
                        }
                    }
                }
            }
    //        printf("ASDF\n");
        }
    }

    */

<!-- /wp:code -->