---
layout: post
title: ZOJ-3950-How Many Nines-思维+模拟
date: 2019-05-08
tags: ["题解"]
---

<!-- wp:paragraph -->

代码极长，WA了三次，第一次忘记了同年的情况，第二次忘记了同月的情况，第三次是有一个地方忘了润年平年分情况。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

好垃圾的代码，打了5个表，结果好好没有发挥它的用处。。。后面一堆分类判断应该写函数的。。。好菜

<!-- /wp:paragraph -->

<!-- wp:image {"id":266,"width":1109,"height":28} -->
<figure class="wp-block-image is-resized">![](TIM截图20190508220948-1024x26.png)</figure>
<!-- /wp:image -->

<!-- wp:code -->

    #include <bits/stdc++.h>
    using namespace std;

    int mon1[13] = {0,31,29,31,30,31,30,31,31,30,31,30,31};
    int mon2[13] = {0,31,28,31,30,31,30,31,31,30,31,30,31};
    int is_mon[13] = {0,3,3,3,3,3,3,3,3,33,3,3,3};///闰年
    int no_mon[13] = {0,3,2,3,3,3,3,3,3,33,3,3,3};
    struct pp {
        int n9;
        int is;
    } leap[10010];

    int isleap(int year) { //1->29 0->28
        if(year%4 == 0 && year%100 != 0) {
            return 1;
        } else if(year%400 == 0) {
            return 1;
        }
        return 0;
    }

    void fff() {
        int flag = 0;
        int n = 0;
        for(int i = 2000 ; i <= 9999 ; i++) {
            leap[i].is = isleap(i);
            n = i;
            while(n) {
                flag = n%10;
                if(flag == 9) {
                    leap[i].n9++;
                }
                n /= 10;
            }
        }
    }

    int main() {
        int n;
        int y1,y2,m1,m2,d1,d2;
        fff();
    //    for(int i = 2000 ; i <= 9999 ; i++){
    //        printf("%d %d %d\n",i,leap[i].is,leap[i].n9);
    //    }
        scanf("%d",&n);
        int sum = 0;
        int is_y = 30 + 33 + 3;
        int no_y = 30 + 33 + 2;
        int is_yy = 366;
        int no_yy = 365;
        while(n--) {
            sum = 0;
            scanf("%d %d %d %d %d %d",&y1,&m1,&d1,&y2,&m2,&d2);
            if(y1 == y2 && m1 == m2) { ///同年同月
                if(d1 <= 9) {
                    if(d2 >= 29) {
                        sum += 3;
                    } else if(d2 >= 19) {
                        sum += 2;
                    } else if(d2 >= 9) {
                        sum += 1;
                    }
                } else if(d1 <= 19) {
                    if(d2 >= 29) {
                        sum += 2;
                    } else if(d2 >= 19) {
                        sum += 1;
                    }
                } else if(d1 <= 29) {
                    if(d2 >= 29) {
                        sum += 1;
                    }
                }

                if(m1 == 9)
                    sum += d2 - d1 + 1;
                sum += leap[y1].n9 * (d2-d1+1);
                printf("%d\n",sum);
                continue;
            }

            if(y1 != y2) {         ///年份不同
                for(int i = y1+1 ; i <= y2-1 ; i++) {
                    if(leap[i].is == 1) {
                        sum += is_y;
                    } else
                        sum += no_y;

                    if(leap[i].is) {
                        sum += leap[i].n9 * is_yy;
                    } else {
                        sum += leap[i].n9 * no_yy;
                    }
                }

                int num1 = 0,num2 = 0;
                for(int i = m1+1 ; i <= 12; i++) {
                    if(leap[y1].is) {
                        sum += is_mon[i];
                        num1 += mon1[i];
                    } else {
                        sum += no_mon[i];
                        num1 += mon2[i];
                    }
                }
                if(leap[y1].is){
                    num1 += mon1[m1] - d1 + 1;
                }
                else{
                    num1 += mon2[m1] - d1 + 1;
                }
                sum += leap[y1].n9 * num1;

                for(int i = 1 ; i <= m2-1 ; i++) {
                    if(leap[y2].is) {
                        sum += is_mon[i];
                        num2 += mon1[i];
                    } else {
                        sum += no_mon[i];
                        num2 += mon2[i];
                    }
                }
                num2 += d2;
                sum += leap[y2].n9 * num2;

            } else {    ///年份相同
                int num = 0 ;
                if(leap[y1].is) {
                    for(int i = m1+1 ; i<= m2-1 ; i++) {
                        num += mon1[i];
                    }
                    num += mon1[m1] - d1 + 1;
                } else {
                    for(int i = m1+1 ; i<= m2-1 ; i++) {
                        num += mon2[i];
                    }
                    num += mon2[m1] - d1 + 1;
                }
                num += d2 ;
                sum += num * leap[y1].n9 ;
                for(int i = m1+1 ; i <= m2-1 ; i++) {
                    if(leap[y2].is) {
                        sum += is_mon[i];
                    } else {
                        sum += no_mon[i];
                    }
                }
            }

    //        printf("%d\n",sum);
            if(leap[y1].is == 0) {
                if(m1 == 2) {
                    if(d1 <= 9) {
                        sum += 2;
                    } else if(d1 <= 19) {
                        sum += 1;
                    } else
                        ;
                } else if(m1 == 9) {
                    if(d1 <= 9) {
                        sum += 3;
                    } else if(d1 <= 19) {
                        sum += 2;
                    } else if(d1 <= 29) {
                        sum += 1;
                    }
                    sum += 30 - d1 + 1;
                } else {
                    if(d1 <= 9) {
                        sum += 3;
                    } else if(d1 <= 19) {
                        sum += 2;
                    } else if(d1 <= 29) {
                        sum += 1;
                    }
                }
            } else {
                if(m1 == 2) {
                    if(d1 <= 9) {
                        sum += 3;
                    } else if(d1 <= 19) {
                        sum += 2;
                    } else
                        sum += 1;
                } else if(m1 == 9) {
                    if(d1 <= 9) {
                        sum += 3;
                    } else if(d1 <= 19) {
                        sum += 2;
                    } else if(d1 <= 29) {
                        sum += 1;
                    }
                    sum += 30 - d1 + 1;
                } else {
                    if(d1 <= 9) {
                        sum += 3;
                    } else if(d1 <= 19) {
                        sum += 2;
                    } else if(d1 <= 29) {
                        sum += 1;
                    }
                }
            }

    //        printf("%d\n",sum);
            if(leap[y2].is == 0) {
                if(m2 == 2) {
                    if(d2 >= 19) {
                        sum += 2;
                    } else if(d2 >= 9) {
                        sum += 1;
                    } else
                        ;
                } else if(m2 == 9) {
                    if(d2 >= 29) {
                        sum += 3;
                    } else if(d2 >= 19) {
                        sum += 2;
                    } else if(d2 >= 9) {
                        sum += 1;
                    }
                    sum += d2;
                } else {
                    if(d2 >= 29) {
                        sum += 3;
                    } else if(d2 >= 19) {
                        sum += 2;
                    } else if(d2 >= 9) {
                        sum += 1;
                    }
                }
            } else {
                if(m2 == 2) {
                    if(d2 >= 29) {
                        sum += 3;
                    } else if(d2 >= 19) {
                        sum += 2;
                    } else if(d2 >= 9) {
                        sum += 1;
                    } else
                        ;
                } else if(m2 == 9) {
                    if(d2 >= 29) {
                        sum += 3;
                    } else if(d2 >= 19) {
                        sum += 2;
                    } else if(d2 >= 9) {
                        sum += 1;
                    }
                    sum += d2;
                } else {
                    if(d2 >= 29) {
                        sum += 3;
                    } else if(d2 >= 19) {
                        sum += 2;
                    } else if(d2 >= 9) {
                        sum += 1;
                    }
                }
            }
            printf("%d\n",sum);
        }
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

虽然很菜，但这是我努力的结果，谁都不能否定！

<!-- /wp:paragraph -->