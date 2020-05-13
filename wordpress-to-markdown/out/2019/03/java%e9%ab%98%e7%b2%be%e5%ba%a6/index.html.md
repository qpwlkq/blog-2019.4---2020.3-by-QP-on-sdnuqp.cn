---
layout: post
title: JAVA高精度
date: 2019-03-29
tags: ["基础__JAVA"]
---

<!-- wp:heading {"level":3} -->

### 偶尔会遇到大数的题，Java首选，C++char数组模拟也可以（从第一位开始遍历，逢十进一即可）

<!-- /wp:heading -->

<!-- wp:paragraph -->

HDUOJ 1002 A + B Problem II(大数加法)

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    import java.util.*;
    import java.math.*;

    public class Main
    { 
         public static void main(String args[]) 
         { 
             Scanner in=new Scanner (System.in);

             int i,n=in.nextInt();

             BigInteger a,b,c;

             for(i=1; i<=n; i++){
             if(i!=1)
                 System.out.println("");
             a=in.nextBigInteger();
             b=in.nextBigInteger();

             c=a.add(b);
             System.out.println("Case "+i+":");
             System.out.println(a+" + "+b+" = "+c);
             }  
         } 
    } 

<!-- /wp:code -->

<!-- wp:paragraph -->

这个题是最简单的Java大数了，

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

其次是HDUOJ 1042 N！

<!-- /wp:paragraph -->

<!-- wp:code -->

    import java.io.*;
    import java.math.*;
    import java.util.*;
    import java.text.*;

    public class Main
    { 
         public static void main(String args[]) 
         { 
    //       Scanner in = new Scanner(System.in);
             Scanner in = new Scanner (new BufferedInputStream(System.in));
             while (in.hasNextInt()){
                 int i,n = in.nextInt();
    //           BigInteger sum = BigInteger.valueOf(1);
                 BigInteger sum = new BigInteger("1");
                 for(i = 2; i <= n ; i++) {
                     BigInteger z  = BigInteger.valueOf(i);
                     sum = sum.multiply(z);
                 }
                 System.out.println(sum);
             }
         } 
    } 

<!-- /wp:code -->

<!-- wp:paragraph -->

Java小白做了两个题，略有体会。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

看网上说，BigInteger和BigDecmial两个类理论上可以求超级大超级大的一个数，最大值取决于你电脑内存！！！！！！！！！！纽币！

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

BigInter 可以看作是一种数据类型，从C++角度来看。。。。。菜。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

声明一个变量a：

<!-- /wp:paragraph -->

<!-- wp:code -->

        BigInteger a;

<!-- /wp:code -->

<!-- wp:paragraph -->

对a赋值有两种方式：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

第一种：

<!-- /wp:paragraph -->

<!-- wp:code -->

        a = new BigInteger("123");
        //"123"是一个字符串，将字符串转化成一个数字

<!-- /wp:code -->

<!-- wp:paragraph -->

第二种：

<!-- /wp:paragraph -->

<!-- wp:code -->

        a = BigInteger.valueOf(i); 
        //这里的i就是一个数，可以用于for循环

<!-- /wp:code -->

<!-- wp:paragraph -->

大数的加减乘除是通过四个"函数"，貌似叫方法，没学过不懂。

<!-- /wp:paragraph -->

<!-- wp:code -->

        a = a.add(BigInteger other);//加
        a = a.multiply(BigInteger other);//乘
        a = a.subtract(BigInteger other);//减
        a = a.divide(BigInteger other);//除

<!-- /wp:code -->

<!-- wp:paragraph -->

还有一些东西，详见

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[[https://blog.csdn.net/Young_12138/article/details/68498724](https://blog.csdn.net/Young_12138/article/details/68498724)]()

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

[[https://blog.csdn.net/suyebiubiu/article/details/78511556](https://blog.csdn.net/suyebiubiu/article/details/78511556)]()

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 大浮点数BigDecimal

<!-- /wp:heading -->

<!-- wp:paragraph -->

HDU 1753

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

代码：

<!-- /wp:paragraph -->

<!-- wp:code -->

    import java.io.*;
    import java.math.*;
    import java.util.*;
    import java.text.*;

    public class Main{
        public static void main(String args[]) {
            Scanner in = new Scanner (new BufferedInputStream(System.in));
            BigDecimal a , b;
            while(in.hasNextBigDecimal()) {
                a = in.nextBigDecimal();
                b = in.nextBigDecimal();
                System.out.println(a.add(b).stripTrailingZeros().toPlainString());
            }   
        }
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

顺带一提，开数组：

<!-- /wp:paragraph -->

<!-- wp:code -->

        BigInteger a[] = new BigInteger[100];

<!-- /wp:code -->