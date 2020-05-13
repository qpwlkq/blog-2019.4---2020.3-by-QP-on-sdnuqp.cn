---
layout: post
title: SDNUOJ-1213-金额的中文大写-模拟
date: 2019-08-14
tags: ["OJ__SDNUOJ"]
---

<!-- wp:paragraph -->

真恶心哦，这个题数据很水，我有个地方写错了也A了，当然，接着改过来了，后面代码是完美的（像00000.00这种李XX出的250样例当然过不了）

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这个题思路是这样的：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

首先最大是亿，所以数最大有12位(整数部分)，所以我将输入数字(字符串读入)存在一个数组中，然后3个for循环遍历1->4 , 5 -> 8 , 9 -> 12 ，为什么要这样呢，因为，我们可以发现，每一段的输出规则是一样的，只不过在每一段后面加了一个"亿"或者"万"，请看样例：

<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">input:
12345678900.23

output:
壹佰贰拾叁亿肆仟伍佰陆拾柒万捌仟玖佰元贰角叁分</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->

我们可以发现输出分解一下就是：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

壹佰贰拾叁      亿    肆仟伍佰陆拾柒     万     捌仟玖佰元     贰角叁分

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

每一部分对应着：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

123     4567     8900     .23

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这时候我们就可以写代码了。情况只有4种而已，注意要在开头是10的时候输出"拾"，而不是"一拾"，top变量标记开始。

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int vis[100];
    char s[100];
    char ss[100];
    map<int, string>mp;
    map<char, string>mmp;

    int main() {
        mp[4] = "";
        mp[3] = "拾";
        mp[2] = "佰";
        mp[1] = "仟";
        mmp['0'] = "零";
        mmp['1'] = "壹";
        mmp['2'] = "贰";
        mmp['3'] = "叁";
        mmp['4'] = "肆";
        mmp['5'] = "伍";
        mmp['6'] = "陆";
        mmp['7'] = "柒";
        mmp['8'] = "捌";
        mmp['9'] = "玖";
        while (gets(s)) {
            int top = 1;
            memset(vis, 0, sizeof vis);
            for (int i = 1; i <= 30; i++) {
                ss[i] = '\0';
            }
            int flag = 0;
            int idx = strlen(s);
            for (int i = 0; i < strlen(s); ++i) {
                if (s[i] == '.') {
                    flag = 1;
                    idx = i;
                    break;
                }
            }
            int cnt = 12;
            for (int i = idx - 1; i >= 0; i--) {
                ss[cnt] = s[i];
                cnt--;
            }

            //printf("no.1\n");
            int fl1 = 0;
            for (int i = 1; i <= 4; i++) {
                if (ss[i] != '\0') {
                    if(top){
                        top = 0;
                        if(ss[i] == '1' && i ==  3){
                            cout << "拾";
                            continue;
                        }
                    }
                    if (ss[i] != '0') {
                        cout << mmp[ss[i]] ;
                        cout << mp[i] ;
                    }
                    else {
                        if (ss[i + 1] != '0' && ss[i+1] != '\0') {
                            cout << "零" ;
                        }
                    }
                    fl1 = 1;
                }
            }
            if (fl1)
                cout << "亿";

            int fl2 = 0;
            for (int i = 5; i <= 8; i++) {
                if (ss[i] != '\0') {
                    if(top){
                        top = 0;
                        if(ss[i] == '1' && i == 7){
                            cout << "拾";
                            continue;
                        }
                    }
                    if (ss[i] != '0') {
                        cout << mmp[ss[i]];
                        cout << mp[i - 4];
                    }
                    else {
                        if (ss[i + 1] != '0' && ss[i+1] != '\0') {
                            cout << "零";
                        }
                    }
                    fl2 = 1;
                }
            }
            if (fl2)
                cout << "万";

            for (int i = 9; i <= 12; i++) {
                if (ss[i] != '\0') {
                    if(top){
                        top = 0;
                        if(ss[i] == '1' && i == 11){
                            cout << "拾";
                            continue;
                        }
                    }
                    if (ss[i] != '0') {
                        cout << mmp[ss[i]];
                        cout << mp[i - 8];
                    }
                    else {
                        if (ss[i + 1] != '0' && ss[i+1] != '\0') {
                            cout << "零";
                        }
                    }
                    fl1 = 1;
                }
            }
            cout << "元";
            if (flag) {
                for (int i = idx + 1; i < strlen(s); i++) {
                    cout << mmp[s[i]];
                    if (i == idx + 1)
                        if(s[i] == '0')
                            ;
                        else
                            cout << "角";
                    else
                        cout << "分";
                }
            }
            else
                cout << "整";
            cout << '\n';
        }
        return 0;
    }

    /*

    12345678900.23

    */

<!-- /wp:code -->