---
layout: post
title: 汇编语言学习(day2)
date: 2020-01-31
tags: ["基础__STL"]
---

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">二. 寄存器(cpu工作原理)
 概述{
     1. cpu内部通讯
     2. cpu主要有运算器, 控制器, 寄存器等器件,这些器件靠 内部总线 相连.
     3. 8086cpu有14个寄存器 : AX, BX, CX, DX, SI, DI, SP, BP, IP, CS, SS, DS, ES, PSW
 }
 2.1 通用寄存器{
     1. 大部分cpu都有8个通用寄存器(AX,BX,CX,DX,都可以分成两个8位寄存器, AX : AH(high高地址: 8 - 16) + AL(low低地址: 0 - 7))
     2. 一个字两个字节, 这个奇怪单位来源就可见一斑了.
 }
 2.2 字在寄存器中的存储{
     ...
 }
 2.3 汇编指令{
     1. 不区分大小写, 大小写不敏感
     2. 几条指令{
         mov ax, 18 -> ax = 18      -> ax寄存器中的值赋值为18
         mov ah, 78 -> ah = 78      -> ah寄存器中的值赋值为78
         add ax, 8  -> ax = ax + 18 -> ax寄存器中的值+8
         mov ax, bx -> ax = bx      -> 将bx寄存器中的值送入ax寄存器
         add ax, bx -> ax = ax + bx -> 将ax, bx中的值相加, 然后赋给ax
     }
     3. 易错点1: 请看这条指令 mov bx, ax (ax = 8226H, bx = 8226H){
         8226H + 8226H = 1044CH, 是个5位数, 而十六位寄存器只能存4位, 所以bx = 044CH
         而多出来的一位1, 被存放到了其他地方, 以后再说. (姑且称为进制位存放寄存器)
     }
     4. 易错点2: 请看这条指令 add al,93H(al = 85H){
         前面说了, AL是AX的低位, 8位寄存器, 我们知道AX = AL + AH
         93H + 85H = 158H, 三位数, 类似第三条, 又是多出一位
         这个多出的1位, 不是! 不是! 不是! 存放在AH中, AL 和 AH虽然连着, 但规则没那么简单, 不要想当然.
         存放到了哪里, 以后再说.
     }
 }
 2.4 物理地址</pre>
<!-- /wp:preformatted -->