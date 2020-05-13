---
layout: post
title: 获取键入值（_kbhit()函数）
date: 2019-04-04
tags: ["杂项"]
---

<!-- wp:paragraph -->

该函数包含在头文件conio.h中，注意这个头文件并不是一个C标准库中的头文件，也就是说bits/stc++.h中没有它。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

函数返回一个数值，称为键码，每个键位均对应着一个键码。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

与_getch()配合使用

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    #include <conio.h>
    using namespace std;

    int main() {
        int x ;
        while(1) {
            if(_kbhit()) {
                x = _getch();
                cout<<x<<'\n';
                if(x == 27) {
                    break;
                }
            }
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:image -->
<figure class="wp-block-image">![](508750-20170504102336211-524432927.png)</figure>
<!-- /wp:image -->