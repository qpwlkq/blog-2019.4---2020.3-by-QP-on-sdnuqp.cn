---
layout: post
title: string成员函数or操作整理
date: 2019-03-29
tags: ["字符串__基础"]
---

<!-- wp:heading {"level":1} -->

# 字符串这个东西嗯~ o(_￣▽￣_)o有点意思丫

<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->

### 首先是c++特有的 string 类：

<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->

#### 1.只能用cin和cout或scanf和printf，不然会得到一堆乱码。（cin以空格和回车为结束，不会吃空格和回车）

<!-- /wp:heading -->

<!-- wp:heading {"level":5} -->

##### 1-1.这两种都可以输入输出，虽然会输出，但是有问题，不能这么用，用scanf时不能进行加操作，为了不超时，尽量用char[]吧；

<!-- /wp:heading -->

<!-- wp:code -->

        scanf("%s",s);
        printf("%s",s);

        scanf("%s",&s);
        printf("%s",s);

<!-- /wp:code -->

<!-- wp:code -->

        scanf("%s",&s);
        cout<<s;
        //没输出

<!-- /wp:code -->

<!-- wp:code -->

        cin>>s;
        printf("%s",s);
        //乱码

<!-- /wp:code -->

<!-- wp:heading {"level":3} -->

### 2.string类可以加，加另一个字符串（也可以加自己）或一个字符，这很好使（不可以减）。

<!-- /wp:heading -->

<!-- wp:code -->

        cin>>s;
        cin>>s1;
        s+=s1;
        cout<<s;

<!-- /wp:code -->

<!-- wp:heading {"level":3} -->

### 3.string类成员函数，前方高能？

<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->

#### 3-1. s.assign（）貌似是和"="一个作用？

<!-- /wp:heading -->

<!-- wp:paragraph -->

其实它有更重要的功能！！！上代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

        s2="WEW";
        s.assign(s2,0,2);
        cout<<s;//输出"WE";

<!-- /wp:code -->

<!-- wp:paragraph -->

s.assign(s2,a,b);

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

意思是s取s2的从a开始往后数b-1个，共b个，这段字符串，好用！（越界也可以，至于有没有影响，我也不知Orz）（注意！！！这里不是a到b，而是a到a+b-1间的字符串！）

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-2 好了，第一个函数讲完了，下一个是s.swap()

<!-- /wp:heading -->

<!-- wp:paragraph -->

这个猫屎没多大卵用。。

<!-- /wp:paragraph -->

<!-- wp:code -->

        s2= "01234567";
        s = "abcdefgh";
        s.swap(s2);
        cout<<s2<<'\n';
        cout<<s;

<!-- /wp:code -->

<!-- wp:paragraph -->

交换两个字符串内容，注意，括号里不能是"XXXXX",只能是已经定义过的一个s（可以是空的）；

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-3 s.append()函数和s.push_back()函数

<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->

#### 3-3-1-1 在s后添加一段字符串，代码：

<!-- /wp:heading -->

<!-- wp:code -->

        s2= "0123456789";
        s1= "ABCDEFGH";
        s = "abcdefgh";
        s1.append(s2,8,1);
        s2.append(s2,8,2);
        cout<<s1;
        cout<<'\n';
        cout<<s2;
        //输出：
        //ABCDEFGH8
        //012345678989

<!-- /wp:code -->

<!-- wp:paragraph -->

注意，可以在s后添加一段s自己中的一段，当然全添加也可以。append（s,a,b）规则同上

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-3-1-2 s.append(a,chr)

<!-- /wp:heading -->

<!-- wp:paragraph -->

chr是一个char字符，不能是一个字符串！意为在字符串s后面加 a 个字符chr。。。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-3-2 push_back()函数

<!-- /wp:heading -->

<!-- wp:paragraph -->

s.push_back(chr);，这个函数单纯的在字符串s后面添加一个字符。NO字符串。功能比较简单。。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 3-4 s.clear()和s.erase

<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->

#### 3-4-1 s.clear()

<!-- /wp:heading -->

<!-- wp:paragraph -->

s.clear()函数貌似比较复杂，像endl一样并不只是换行，它并不是只是清空，还有其他不知道的神奇操作。。。。。看网上有很多人踩坑，出现各种问题，我。。。菜鸡。。不懂。。。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-4-2 s.erase()

<!-- /wp:heading -->

<!-- wp:paragraph -->

这个函数较为灵活，有两个用法

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

首先是，看代码

<!-- /wp:paragraph -->

<!-- wp:code -->

        s2= "0123456789";
        s2.erase(5);
        cout<<s2;//输出01234

<!-- /wp:code -->

<!-- wp:paragraph -->

将5位置之后的删去，包括5。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

然后是，看代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

        // 从位置pos=6处开始，共删除4个字符
        s.erase(6, 4);

<!-- /wp:code -->

<!-- wp:paragraph -->

删除中间一段可以用这个函数，很好使！

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 3-5 reverse函数（这个不是成员函数）

<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->

### 3-5-1 string

<!-- /wp:heading -->

<!-- wp:paragraph -->

这个函数可以用于string和char数组，也是对string来说比较好使常用的几个函数之一。

<!-- /wp:paragraph -->

<!-- wp:code -->

        s="0123456789";
        cout<<s<<'\n';
        reverse(s.begin(),s.end());
        cout<<s<<'\n';
        reverse(s.begin(),s.end()-5);
        cout<<s;

<!-- /wp:code -->

<!-- wp:paragraph -->

输出：

<!-- /wp:paragraph -->

<!-- wp:code -->

       0123456789
       9876543210
       5678943210

<!-- /wp:code -->

<!-- wp:paragraph -->

通过迭代器来决定那段反转，可以部分反转，范围前闭后开。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 3-5-2 char

<!-- /wp:heading -->

<!-- wp:code -->

        char s[10]={'0','1','2','3','4'};
        reverse(s,s+3);
        printf("%s",s);

<!-- /wp:code -->

<!-- wp:paragraph -->

可以部分反转，前闭后开，reverse(s+a,s+b)表示s[a]到s[b-1]反转

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 3-6 s.find()

<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->

#### 3-6-1 s.find(s1)/s.find(chr)

<!-- /wp:heading -->

<!-- wp:paragraph -->

首先，如果找到它返回子串（或字符）在母串中第一次出现的首字符下标值，否则返回npos，这个东西有的编译器取值4294967295，有的取值-1，在字符串中找不到子串 (或字符)。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

也可以 s.find(s1,5);表示查找在下标5（包括5）后子串（字符）出现的位置，未找到返回npos

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-6-2 s.find_first_of()/s.find_last_of()

<!-- /wp:heading -->

<!-- wp:paragraph -->

查找首次出现的位置和最后一次出现的位置，也可以像3-6-1中第二点一样，选择在某位置后查找

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-6-2 s.rfind()!!!反向查找子串

<!-- /wp:heading -->

<!-- wp:paragraph -->

注意，这个函数不会变绿，与s.find()结合使用，可以判断子串在母串中是否是唯一的。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 3-7 s.substr()

<!-- /wp:heading -->

<!-- wp:paragraph -->

s.substr(s1,n)和assign函数很像，规则也相同，看前面吧。

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 3-8 s.size()

<!-- /wp:heading -->

<!-- wp:paragraph -->

返回长度

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 3-9 s.replace()

<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->

#### 3-9-1 前方高能?!这是一个字符串置换函数，可以将母串某一段换成另一串字符串，也可以换成空！！！！不是换成 '\0'，相当于删除了某一段！！！

<!-- /wp:heading -->

<!-- wp:code -->

        s1 = "0123456789";
        s1.replace(1,2,"");
        cout<<s1;//输出：03456789

<!-- /wp:code -->

<!-- wp:paragraph -->

第一个参数是位置，第二个参数是置换一段的长度。//参数也可以是迭代器

<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->

#### 3-9-2 5个参数时，看代码：

<!-- /wp:heading -->

<!-- wp:code -->

        s1 = "0123456789";
        s2 = "qwert";
        s1.replace(1,6,s2,1,3);
        cout<<s1;//输出：0we789

<!-- /wp:code -->

<!-- wp:paragraph -->

后面两个数字表示换成s2的1到3位置子串，男的的一个前闭后闭的函数！！！

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

嗯~ o(_￣▽￣_)o差不多够使了。。。。 欧克。  

<!-- /wp:paragraph -->