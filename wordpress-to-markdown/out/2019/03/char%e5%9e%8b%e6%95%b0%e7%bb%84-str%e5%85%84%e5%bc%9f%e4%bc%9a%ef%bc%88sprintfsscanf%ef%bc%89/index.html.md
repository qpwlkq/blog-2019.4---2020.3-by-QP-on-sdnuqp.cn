---
layout: post
title: char型数组 & str兄弟会（sprintf&sscanf）
date: 2019-03-29
tags: ["字符串__基础"]
---

<!-- wp:heading {"level":1} -->

# char型数组也是很有意思的东西，它像string一样有很多函数or操作or算法

<!-- /wp:heading -->

<!-- wp:paragraph -->

尽量不要用gets()函数输入，这是个哲学问题。。。。。。Orz

<!-- /wp:paragraph -->

<!-- wp:heading -->

## 1-1 sscanf和sprintf函数，面向字符串的输入输出流

<!-- /wp:heading -->

<!-- wp:paragraph -->

在我看来就是从字符串中输入数据，而不是像scanf从键盘键入数据。详见百度百科

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 1-1-1 sscanf函数

<!-- /wp:heading -->

<!-- wp:paragraph -->

_sscanf 读取格式化的字符串中的数据_--百度百科

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

TA常用来字符串和数字的转换，很好使，不用自己系一大堆代码了。Orz。。。

<!-- /wp:paragraph -->

<!-- wp:code -->

    int main(){    
    //    s="0123456789";

        char ss[100]="123abc(DEFghijk)";
        char sss[100]="z123abc(DEFghijk)";
        char ss1[100];
        char ss2[100];
        char ss3[100];
        char ss4[100];
        char ss5[100];
        sscanf(ss,"%s",ss1);//1
        sscanf(ss,"%8s",ss2);//2
        sscanf(ss,"%[^(]",ss3);//3
        sscanf(ss,"%[^a-z]",ss4);//4
        sscanf(ss,"%[1-9,a-z,A-Z,(]",ss5);//5

        int x;
        cout<<x<<'\n';

        sscanf(ss,"%d",&x);///传地址

        cout<<x<<'\n';
        puts(ss1);
        puts(ss2);
        puts(ss3);
        puts(ss4);
        puts(ss5);
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

输出：

<!-- /wp:paragraph -->

<!-- wp:code -->

    0
    123
    123abc(DEFghijk)
    123abc(D
    123abc
    123
    123abc(DEFghijk

<!-- /wp:code -->

<!-- wp:paragraph -->

这个函数中间参数有很多，什么转化为16进制，8进制之类的，我觉得大概大学期间用不了几次。。。。菜。。。。Orz。。。。。就不说了，只说说对ACM有用的吧。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

（上面代码有标号） 1号行代码：ss是一个字符串，然后"%s"意思是转化为字符串,然后赋给ss1，作用就是 '=' 。如果中间使"%d",那么就会起到字符串转化数字的作用了，实例中得到整数123，赋给ss1,ss1是char类型，"{"的ASCII码是123，所以字符串ss1就是单个字符"{".

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

2号行代码："%8s"中间的数字8表示从头开始，一共取8个字符。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

3号行代码："%[^(]"表示读到'（'结束，注意里面不要乱打空格，%[^ ]表示到空格结束，读不进空格。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

4号行代码："%[^a-z]"表示读到小写字母就结束，小写字母读不进。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

"^"符号表示到什么符号停止，大概就是非的意思。"%[]"这玩意貌似叫字符集

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

5号行代码：%[a-z,A-Z,0-9]意思是读小写,大写字母,数字0-9，后面加个"，"还可以继续加可读入符号。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 1-1-2 sprintf函数

<!-- /wp:heading -->

<!-- wp:paragraph -->

_sprintf指的是字符串格式化命令，主要功能是把格式化的数据写入某个字符串中_--百度百科

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

主要作用与sscanf相反，是将数字转变成字符串，代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

        sprintf(ss1,"%d",123);
        sprintf(ss2,"%4d%4d",123,456);
        puts(ss1);
        puts(ss2);

<!-- /wp:code -->

<!-- wp:paragraph -->

输出：

<!-- /wp:paragraph -->

<!-- wp:code -->

    123
     123 456

<!-- /wp:code -->

<!-- wp:paragraph -->

与printf类似，只不过sprintf是打印到一个字符串罢了

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

详见：[sprintf](https://blog.csdn.net/oyhb_1992/article/details/75095472)

<!-- /wp:paragraph -->

<!-- wp:heading -->

## 1-2 以atoi函数为代表的一系列函数，C标准库函数

<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->

### 1-2-1 atoi()函数，ascii to integer

<!-- /wp:heading -->

<!-- wp:paragraph -->

作用是将字符串转化为整型数，未执行有效转换则返回0，比喻说字符串中全是字母时。。

<!-- /wp:paragraph -->

<!-- wp:code -->

        char ss4[100]="1234asdf";
        char ss5[100]="asdf1234";
        int x=atoi(ss4);
        int x1=atoi(ss5);
        printf("%d\n",x);
        printf("%d",x1);

<!-- /wp:code -->

<!-- wp:paragraph -->

输出：

<!-- /wp:paragraph -->

<!-- wp:code -->

    1234
    0

<!-- /wp:code -->

<!-- wp:heading {"level":3} -->

### 1-2-2 atof()函数，。。。to f 浮点数

<!-- /wp:heading -->

<!-- wp:code -->

        char ss4[100]="1234.1234";
        char ss5[100]="asdf1234";
        double x=atof(ss4);
        double x1=atof(ss5);
        printf("%lf\n",x);
        printf("%lf",x1);

<!-- /wp:code -->

<!-- wp:paragraph -->

输出：

<!-- /wp:paragraph -->

<!-- wp:code -->

    1234.123400
    0.000000

<!-- /wp:code -->

<!-- wp:heading {"level":3} -->

### 1-2-3 atol()函数 ，长整型

<!-- /wp:heading -->

<!-- wp:code -->

        char ss3[100]="-2147483648";
        char ss4[100]="2147483647";
        char ss5[100]="asdf1234";
        long long int x0=atol(ss3);
        long long int x=atol(ss4);
        long long int x1=atol(ss5);
        printf("%lld\n",x0);
        printf("%lld\n",x);
        printf("%lld",x1);
        //输出：
        //-2147483648
        //2147483647
        //0

<!-- /wp:code -->

<!-- wp:paragraph -->

这个函数我试着有点问题，超出int范围之后，返回的数就很哲学。。。。。。。Orz

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

！！！

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 1-3 tolower() and toupper()

<!-- /wp:heading -->

<!-- wp:code -->

        char c='C';
        c=tolower(c);
        putchar(c);
        cout<<'\n';
        c=toupper(c);
        putchar(c);

<!-- /wp:code -->

<!-- wp:paragraph -->

tolower转换成小写字母，toupper转换成大写字母，括号中的参数应该是一个int型数，字符c自动转化成ascii码。不嫌麻烦可以用来赋值。。。。。

<!-- /wp:paragraph -->

<!-- wp:code -->

        char c='C';
        c=toupper(65);
        putchar(c);
        //输出A

<!-- /wp:code -->

<!-- wp:paragraph -->

真是闲的。。。Orz。。

<!-- /wp:paragraph -->

<!-- wp:heading -->

## 1-4 重点来了，一堆str开头的函数。。。。前方高能，好累。。。

<!-- /wp:heading -->

<!-- wp:list -->

*   strcat() 字符串拼接函数
*   strncat() 字符串拼接函数（拼接指定部分）
*   strcmp() 字符串比较函数
*   strncmp() 字符串比较函数（比较指定长度）
*   strnicmp() 字符串比较函数（比较制定长度，不区分大小写）
*   strlwr() 将大写转化为小写
*   strupr() 将小写转化为大写
*   strcpy() 字符串拷贝函数
*   strncpy() 字符串拷贝函数（有3个参数，第一个目录字符串、第二个源字符串，第三个是一个整数)
*   strlen() 计算字符串长度函数
*   strchr() 查找字符串中某字符第一次出现位置函数
*   strrchr() 查找字符串中某字符最后一次出现位置函数
*   strspn() 返回s1中第一个在s2中不存在的字符的索引(find_first_not_of)
*   strcspn() 返回s1中第一个也在s2中存在的字符的索引(find_first_of)
*   strdup() 将串拷贝到新建的位置处(返回一个指针,指向为复制字符串分配的空间;如果分配空间失败,则返回NULL值。需要用free()释放相应的内存空间，否则会造成内存泄漏。赶脚基本没用)
*   strrev() 字符串反转函数（注意！非C标准库函数，没卵用，还很危险）
*   strstr() 查找子串出现位置函数
*   strtok() 从串s1中分离出由串s2中指定的分界符分隔开的记号(token)(很复杂，基本没用)
*   strtol() 将字符串转化为长整型数
*   strtod() 将字符串转化为double型
*   strtof() 将字符串转化为flout型
*   strtok() 切割字符串
*   strset() 用某字符填充字符串
<!-- /wp:list -->

<!-- wp:paragraph -->

有的返回下标，有的返回长度，有的返回ture或false，有的返回指针。。。有空再具体填充一下吧  

<!-- /wp:paragraph -->