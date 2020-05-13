---
layout: post
title: 超简易贪吃蛇源码
date: 2019-10-04
tags: ["杂项"]
---

<!-- wp:paragraph -->

闲来无事(不学算法??????)写了一个贪吃蛇小游戏,很简单的只是用了一个获取键盘事件的小函数而已.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

为了确定蛇的位置,蛇头复制4(蛇的长度),蛇尾赋值1,蛇身赋值3到2(如图),然后怎么动呢?每次蛇头移动一格,蛇身的值-1,但是这样时间复杂度高了,每次蛇移动都要循环一次去对蛇身改值,所以我打算放弃这种思路,改而去将蛇头移动后的位置直接赋值为原蛇头位置的值+1,这样就直接省去了蛇身的操作,仅仅更改蛇头,蛇尾即可,但是移动次数收到了限制,要在int范围内,不然就会分崩离析.....

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

对了,为甚么要对蛇每一节赋值,就是为了确定蛇尾的上一节,之后进行蛇尾坐标的更改.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

我的贪吃蛇只能动,还没有加上吃的操作,并且使用OOD写的,没用OOP.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

欢迎复制黏贴运行.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Code :

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    #include <conio.h>
    using namespace std;

    bool vis[11][11];
    int mp[11][11] = {
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 1, 2, 3, 4, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
        0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
    };
    int xt, yt, d = 4;
    int xw, yw;

    int judge(int x, int y) {
        if (x > 10 '' x <= 0 '' y > 10 '' y <= 0 '' vis[x][y])
            return 1;
        return 0;
    }

    int main() {
        int ch1, ch2;
        xt = 5, yt = 4;
        xw = 5, yw = 1;
        while (1) {
            cout << xt << yt << '\n';
            if (judge(xt, yt)) {
                cout << "YOU LOSE!";
                break;
            }
            if (_kbhit()) {
                ch1 = _getch();
                ch2 = _getch();
                //cout << ch1 << " " << ch2 << '\n';
                switch (ch2) {
                case 72:
                    d = 1; //上
                    break;
                case 80:
                    d = 2; //下
                    break;
                case 75:
                    d = 3; //左
                    break;
                case 77:
                    d = 4; //右
                }
            }

            switch (d) {
            case 1:
                mp[xt - 1][yt] = mp[xt][yt] + 1;
                xt -= 1; //上
                break;
            case 2:
                mp[xt + 1][yt] = mp[xt][yt] + 1;
                xt += 1; //下
                break;
            case 3:
                mp[xt][yt - 1] = mp[xt][yt] + 1;
                yt -= 1; //左
                break;
            case 4:
                mp[xt][yt + 1] = mp[xt][yt] + 1;
                yt += 1; //右
            }
            //对尾巴进行操作
            if (mp[xw + 1][yw] == mp[xw][yw] + 1) {
                mp[xw][yw] = 0;
                xw = xw + 1;
            }
            else if (mp[xw - 1][yw] == mp[xw][yw] + 1) {
                mp[xw][yw] = 0;
                xw = xw - 1;
            }
            else if (mp[xw][yw + 1] == mp[xw][yw] + 1) {
                mp[xw][yw] = 0;
                yw = yw + 1;
            }
            else if (mp[xw][yw - 1] == mp[xw][yw] + 1) {
                mp[xw][yw] = 0;
                yw = yw - 1;
            }
            //输出mp
            cout << d << '\n';
            for (int i = 1; i <= 10; i++) {
                for (int j = 1; j <= 10; j++) {
                    if (mp[i][j]) {
                        if (i == xt && j == yt)
                            cout << "O";
                        else
                            cout << "o";
                    }
                    else
                        cout << "#";
                    //cout << ' ';
                }
                cout << '\n';
            }
            _sleep(100);
            system("cls");
        }
        return 0;
    }

<!-- /wp:code -->