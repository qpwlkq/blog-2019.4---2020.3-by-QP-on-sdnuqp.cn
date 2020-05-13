---
layout: post
title: STL—pair
date: 2019-03-29
tags: ["基础__STL"]
---

<!-- wp:paragraph -->

c++中的结构模板，定义在头文件<utility>中，提供一个包含2个数据成员的结构体模板 ---百度百科

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int main(){
        pair<pair<int,pair<int,string> >,pair<int,pair<int,string> > >q1;
        q1.first.first = 1;
        q1.first.second.first = 2;
        q1.first.second.second = "hhh";
        q1.second.first = 3;
        q1.second.second.first = 4;
        q1.second.second.second = "lll";

        cout<< q1.first.first;
        cout<<'\n';
        cout<< q1.first.second.first;
        cout<<'\n';
        cout<< q1.first.second.second;
        cout<<'\n';

        cout<< q1.second.first;
        cout<<'\n';
        cout<< q1.second.second.first;
        cout<<'\n';
        cout<< q1.second.second.second;
        cout<<'\n';

        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

输出：

<!-- /wp:paragraph -->

<!-- wp:code -->

    1
    2
    hhh
    3
    4
    lll

<!-- /wp:code -->

<!-- wp:paragraph -->

pair更像是一个高级点的结构体，了解了这个东西之后就会发现这个东西真好用。。。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int main() {
        int a,b,c,d;
        scanf("%d %d",&a,&b);
        scanf("%d %d",&d,&c);

        pair<int,int >q0;//定义

        pair<int,int >q1(a,b);//定义,并赋值

        pair<int,int >q2 = make_pair(d,c);//创建

        if(q1 < q2)
            printf("若p1.first<p2.first '' p1.second<p2.second 则p1<p2为ture\n");

        if(q1 == q2)
            printf("pair中两个成员依此相等则为ture\n");

        return 0;
    }

<!-- /wp:code -->