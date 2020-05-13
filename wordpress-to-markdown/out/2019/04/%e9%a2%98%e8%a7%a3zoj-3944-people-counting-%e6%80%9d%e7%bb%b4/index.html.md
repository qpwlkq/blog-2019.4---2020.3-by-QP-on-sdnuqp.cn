---
layout: post
title: [题解]ZOJ-3944-People counting-思维
date: 2019-04-15
tags: ["题解"]
---

<!-- wp:paragraph -->

这道题还是不难的，我想的是通过遍历每一个位置，然后对其他位置进行标记，但是WA了  

我写的很复杂，先判断当前位置是身体那一部分，然后对其它部分判断，如果数组对应位置是他对应的身体部分，就标记，不然说明这部分被别人挡住了。  

然而，WA了

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

换了队友敲，一他边过了，我的代码就不管了，太低级了。

<!-- /wp:paragraph -->

<!-- wp:code -->

    AC code：
    #include <bits/stdc++.h>

    using namespace std;
    typedef long long ll;
    const int INF = 0x3f3f3f3f;
    const int N = 1e5;
    char c[105][105];

    bool pd(int i,int j)
    {
        if(c[i][j] == ''')
            return 1;
        if(c[i-1][j] == 'O')
            return 1;
        if(c[i][j-1] == '/')
            return 1;
        if(c[i][j+1] == '\\')
            return 1;
        if(c[i+1][j-1] == '(')
            return 1;
        if(c[i+1][j+1] == ')')
            return 1;
        return 0;
    }

    int main()
    {
        int t;
        cin >> t;
        while(t--)
        {
            memset(c,0,sizeof(c));
            int x,y,sum = 0;
            cin >> x >> y;
            for(int i = 1; i <= x; i++)
            {
                for(int j = 1; j <= y; j++)
                {
                    cin >> c[i][j];
                }
            }
            for(int i = 0; i <= x + 1; i++)
            {
                for(int j = 0; j <= y + 1; j++)
                {
                    if(pd(i,j))
                    {
                        sum++;
                    }
                }
            }
            cout << sum << endl;
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

最好的部分就是这个函数了，非常棒的想法。  
 pd函数，是判断在当前位置是否有个人，就当c[i][j]是他的肚子，最后仍然是遍历。  
 想的太棒了，Orz。(๑•̀ㅂ•́)و✧

<!-- /wp:paragraph -->