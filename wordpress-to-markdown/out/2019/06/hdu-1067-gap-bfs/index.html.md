---
layout: post
title: [专题二：搜索进阶]HDU-1067-GAP-BFS
date: 2019-06-03
tags: ["kuangbin专题","题解"]
---

<!-- wp:code -->

    题不难，输入是一坨屎。

    #include <bits/stdc++.h>
    using namespace std;

    char begin_c[5][9];
    char end_c[4][8] = {
        11,12,13,14,15,16,17,8,
        21,22,23,24,25,26,27,8,
        31,32,33,34,35,36,37,8,
        41,42,43,44,45,46,47,8
    };

    char begin_str[50];
    char end_str[50];

    unordered_map<string, bool>mp;

    struct node {
        char c[40];
        int dir[5];
        int sum;
    };

    bool judge(node p) {

    //    for(int i = 1 ; i < strlen(end_str) ; i++) {
    //        printf("%d ",end_str[i]);
    //    }
    //    printf(">>>\n");
    //    for(int i = 1; i < strlen(p.c) ; i++) {
    //        printf("%d ",p.c[i]);
    //    }
    //    printf("\n");
        if(strcmp(p.c+1,end_str+1) == 0) {
            return 1;
        }
        return 0;
    }

    bool check(char *a, int pos) {
        if((int)a[pos-1]%10 < 7) {
    //        printf("b\n");
            return true;
        }
        return false;
    }

    int find_pos(char *a, int pos) {
        for(int i = 0 ; i < 32 ; i++) {
            if(a[i] == a[pos]+1)
                return i;
        }
    }

    queue<node>q;
    void bfs() {
        node p,t;
        strcpy(p.c, begin_str);
    //    printf("begin:  %d>>\n",strlen(p.c));
    //    for(int j = 0 ; j < strlen(p.c) ; j++) {
    //        printf("%2d ",p.c[j]);
    //        if((j+1)%8 == 0)
    //            printf("\n");
    //    }
    //    printf(">>>>>>>>>>>>>>>\n");
        p.sum = 0;

        int cnt = 1;
        for(int i = 0; i < 32 ; i++) {
            if(p.c[i] == 8) {
                p.dir[cnt++] = i;
            }
        }
        q.push(p);
        int z;
        while(!q.empty()) {
            p = q.front();
            q.pop();
            if(judge(p)) {
                printf("%d\n",p.sum);
                while(!q.empty()) {
                    q.pop();
                }
                return ;
            }
            for(int i = 1; i <= 4 ; i++) {
                strcpy(t.c,p.c);
                memcpy(t.dir, p.dir, sizeof p.dir);
    //            for(int i = 1; i <= 4 ; i++){
    //                printf("%d ",t.dir[i]);
    //            }
    //            printf("\n");

    //            for(int i = 0 ; i <= 31 ; i++) {
    //                printf("%d ",t.c[i]);
    //                if((i+1)%8 == 0)
    //                    printf("\n");
    //            }
    //            printf("sadf\n");
                t.sum = p.sum + 1;
                if(check(t.c,p.dir[i])) {
                    z = find_pos(t.c, p.dir[i]-1);
    //                printf("<%d>\n",z);
                    swap(t.c[z], t.c[t.dir[i]]);
                    t.dir[i] = z;
                    if(mp[t.c] == 0) {
                        mp[t.c] = 1;
    //                    for(int i = 0 ; i < 32 ; i++) {
    //                        printf("%2d ",t.c[i]);
    //                        if((i+1)%8 == 0)
    //                            printf("\n");
    //                    }
    //                    printf(">>>\n");
                        q.push(t);
                    }
                }
            }
        }
        printf("-1\n");
        return ;
    }

    int main() {
        int t;
        int x;
        int cnt;
        scanf("%d",&t);
        while(t--) {
    //        memset(begin_str,'\0',sizeof begin_str);
    //        memset(end_str,'\0',sizeof end_str);
    //        memset(begin_c,'\0',sizeof begin_c);
            mp.clear();

            getchar();
            cnt = 1;
            for(int i = 1 ; i <= 4 ; i++) {
                for(int j = 2 ; j <= 8 ; j++) {
                    scanf("%d",&x);
                    begin_c[i][j] = x;
                    if(begin_c[i][j]%10 == 1) {
                        begin_c[begin_c[i][j]/10][1] = begin_c[i][j];
                        begin_c[i][j] = 8;
                    }
                }
            }

    //        for(int i = 1 ; i <= 4 ; i++){ ///输入测试
    //            for(int j = 1; j <= 8 ; j++){
    //                printf("%2d ",begin_c[i][j]);
    //            }
    //            printf("\n");
    //        }

            cnt = 0;
            for(int i = 1 ; i <= 4 ; i++) {
                for(int j = 1 ; j <= 8 ; j++) {
                    begin_str[cnt++] = begin_c[i][j];
                }
            }

            cnt = 0;
            for(int i = 0 ; i < 4 ; i++) {
                for(int j = 0 ; j < 8 ; j++) {
                    end_str[cnt++] = end_c[i][j];
                }
            }

            mp[begin_str] = true;
    //
    //        for(int i = 0 ; i < 32 ; i++){   ///test
    //            printf("%2d ",begin_str[i]);
    //            if((i+1)%8 == 0)
    //                printf("\n");
    //        }
    //
    //        printf("end_str:\n");
    //        for(int j = 0; j < 32 ; j++){
    //            printf("%2d ",end_str[j]);
    //            if((j+1)%8 == 0)
    //                printf("\n");
    //        }
    //        printf("\n");

            bfs();

        }
    }

    /*

    4

    12 13 14 15 16 17 21
    22 23 24 25 26 27 31
    32 33 34 35 36 37 41
    42 43 44 45 46 47 11

    26 31 13 44 21 24 42
    17 45 23 25 41 36 11
    46 34 14 12 37 32 47
    16 43 27 35 22 33 15

    17 12 16 13 15 14 11
    27 22 26 23 25 24 21
    37 32 36 33 35 34 31
    47 42 46 43 45 44 41

    27 14 22 35 32 46 33
    13 17 36 24 44 21 15
    43 16 45 47 23 11 26
    25 37 41 34 42 12 31

    */

<!-- /wp:code -->