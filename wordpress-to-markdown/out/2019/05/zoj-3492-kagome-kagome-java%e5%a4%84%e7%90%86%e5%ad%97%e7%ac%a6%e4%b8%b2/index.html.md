---
layout: post
title: ZOJ-3492-Kagome Kagome-Java处理字符串
date: 2019-05-05
tags: ["基础__JAVA","题解"]
---

<!-- wp:paragraph -->

Visual code快让我崩溃了。我总是忘记保存，完全没有提示，下次打开，望着一个空文件，凌乱。。。。。。。。。。。。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

用java处理字符串比较麻烦

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

简单读取：

<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">String s = in.nextLine();</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->

但是像下面那个题一样给了几个字符串：XXXX XXX XXXXX  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这就gg了。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

in.nextline直接读一行。  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

这是就要用切割字符串：  

<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">String s = in.nextLine();   
String[] ss = new String[100];    
ss = s.split(" "); ///以" "(空格)作为切割点。  
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->

 切割成的子串只能以字符串数组来接受！

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

例题：

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

ZOJ-3492-Kagome Kagome

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code:

<!-- /wp:paragraph -->

<!-- wp:code -->

    import java.io.*;
    import java.util.*;

    public class Main {
    	public static void main(String[] args) {
    		Scanner in = new Scanner(new BufferedInputStream(System.in));
    		int n;
    		n = in.nextInt();
    		int flag;
    		int z;
    		String s,sss,ssz;
    		String[] sz = new String[110];
    		String[] ss = new String[110];
    		while(n-- >= 1) {
    			z = in.nextInt();
    			ssz = in.nextLine();
    			sz = ssz.split(" ");
    			ssz = sz[1];
    //			System.out.println(z);
    //			System.out.println(sz[1]);
    			flag = 0;
    			sss = in.nextLine();
    			ss = sss.split(" ");
    			for(int i = 0 ; i < ss.length ; i++) {
    				if(ss[i].equals(ssz)) {
    					flag = i + ss.length/2;
    					if(flag >= ss.length) {
    						flag %= ss.length;
    					}
    				}
    			}
    			System.out.println(ss[flag]);
    		}
    	}
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

<!-- /wp:paragraph -->