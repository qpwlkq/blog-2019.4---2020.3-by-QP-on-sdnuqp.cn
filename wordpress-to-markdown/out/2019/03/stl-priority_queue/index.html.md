---
layout: post
title: STL-priority_queue
date: 2019-03-29
tags: ["基础__STL"]
---

<!-- wp:paragraph -->

少废话，直接上代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    struct cmp1{
        bool operator ()(int &a,int &b){
            return a>b;//最小值优先
        }
    };

    struct cmp2{
        bool operator () (int &a,int &b){
            return a<b;//最大值优先
        }
    };

    priority_queue <int >q;

    priority_queue <int ,vector<int >,cmp1>q1;
    priority_queue <int ,vector<int >,cmp2>q2;

    priority_queue <int ,vector<int >,greater<int > >q3;
    priority_queue <int ,vector<int >,less<int > >q4;

    int main(){
        int x;
        for(int i=1;i<=10;i++){
            x = i;
            if(x%2){
                x = 10-i;
            }
            q.push(x);
            q1.push(x);
            q2.push(x);
            q3.push(x);
            q4.push(x);
        }
        while(!q.empty()){
            cout<<q.top()<<' ';
            q.pop();
        }
        cout<<'\n';
        while(!q1.empty()){
            cout<<q1.top()<<' ';
            q1.pop();
        }
        cout<<'\n';
        while(!q2.empty()){
            cout<<q2.top()<<' ';
            q2.pop();
        }
        cout<<'\n';
        while(!q3.empty()){
            cout<<q3.top()<<' ';
            q3.pop();
        }
        cout<<'\n';
        while(!q4.empty()){
            cout<<q4.top()<<' ';
            q4.pop();
        }
        cout<<'\n';
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

输出：

<!-- /wp:paragraph -->

<!-- wp:code -->

     q:  10 9 8 7 6 5 4 3 2 1
    q1:  1 2 3 4 5 6 7 8 9 10
    q2:  10 9 8 7 6 5 4 3 2 1
    q3:  1 2 3 4 5 6 7 8 9 10
    q4:  10 9 8 7 6 5 4 3 2 1

<!-- /wp:code -->

<!-- wp:paragraph -->

另一种：

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    struct number1 {
        int x;
        bool operator < (const number1 &a) const {
            return x>a.x;//最小值优先
        }
    };

    struct number2 {
        int x;
        bool operator > (const number2 &a) const {
            return x<a.x;//最大值优先
        }
    };

    number1 num1[]= {14,10,56,7,83,22,36,91,3,47,72,0};
    number2 num2[]= {14,10,56,7,83,22,36,91,3,47,72,0};

    priority_queue<number1>q5;
    priority_queue<number2>q6;

    int main() {
        int x;
        for(int i=0; num1[i].x; i++)
            q5.push(num1[i]);
        for(int i=0; num2[i].x; i++)
            q6.push(num2[i]);

        printf("q5:  \n");
        while(!q5.empty()) {
            printf("%3d",q5.top());
            q5.pop();
        }
        puts("");
        printf("q6:  \n");
        while(!q6.empty()) {
            printf("%3d",q6.top());
            q6.pop();
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

莫名其妙的报错，跳入stl_function文件

<!-- /wp:paragraph -->

<!-- wp:code -->

      template<typename _Tp>
        struct less : public binary_function<_Tp, _Tp, bool>
        {
          _GLIBCXX14_CONSTEXPR
          bool
          operator()(const _Tp& __x, const _Tp& __y) const
          { return __x < __y; }
        };

<!-- /wp:code -->

<!-- wp:paragraph -->

无力抵抗。。。。。Orz

<!-- /wp:paragraph -->