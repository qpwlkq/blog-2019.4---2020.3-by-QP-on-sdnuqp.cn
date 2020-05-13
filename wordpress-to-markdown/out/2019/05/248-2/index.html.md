---
layout: post
title: ZOJ-4108-Fibonacci in the Pocket-Java大数取余
date: 2019-05-05
tags: ["基础__JAVA","题解"]
---

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">一个模拟，我WA了好几次，崩溃。  
 要注意的是大数取余：  
 BigInteger a = in.nextBigInteger();  
 BigInteger three = BigInteger.valueOf(3);  
 BigInteger num1[] = a.divideAndRemainder(three);  
 用一个数组调用divideAndRemainder方法能够同时获得大数除，和余数。  
 num[0] 是除的结果，num[1] 是余数  
</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->

    AC code:
    import java.io.*;
    import java.math.*;
    import java.util.Scanner;

    public class Main {

    	public static void main(String args[]) {
    		Scanner in = new Scanner(new BufferedInputStream(System.in));
    		int t = in.nextInt();
    		while (t-- >= 1) {
    			BigInteger a = in.nextBigInteger();
    			BigInteger b = in.nextBigInteger();
    			BigInteger num1[] = a.divideAndRemainder((BigInteger.valueOf(3)));
    			BigInteger num2[] = b.divideAndRemainder((BigInteger.valueOf(3)));
    			if (num1[0].compareTo(num2[0]) == 0) {
    				if (num1[1].compareTo(num2[1]) == 0) {
    					if (num1[1].compareTo(BigInteger.valueOf(1)) == 0 '' num2[1].compareTo(BigInteger.valueOf(2)) == 0)
    						System.out.println(1);
    					else if (num1[1].compareTo(BigInteger.valueOf(0)) == 0)
    						System.out.println(0);
    				} else {
    					if ((num1[1].compareTo(BigInteger.valueOf(1)) == 0) && (num2[1].compareTo(BigInteger.valueOf(2)) == 0))
    						System.out.println(0);
    					else if ((num1[1].compareTo(BigInteger.valueOf(1)) == 0) && (num2[1].compareTo(BigInteger.valueOf(0)) == 0))
    						System.out.println(0);
    					else if ((num1[1].compareTo(BigInteger.valueOf(2)) == 0) && (num2[1].compareTo(BigInteger.valueOf(0)) == 0))
    						System.out.println(1);
    				}
    				continue;
    			}
    			if (num1[1].compareTo(BigInteger.valueOf(1)) == 0) {
    				if (num2[1].compareTo(BigInteger.valueOf(1)) == 0) {
    					System.out.println(1);
    				} else if (num2[1].compareTo(BigInteger.valueOf(2)) == 0) {
    					System.out.println(0);
    				} else {
    					System.out.println(0);
    				}
    			} else if (num1[1].compareTo(BigInteger.valueOf(2)) == 0) {
    				if (num2[1].compareTo(BigInteger.valueOf(1)) == 0) {
    					System.out.println(0);
    				} else if (num2[1].compareTo(BigInteger.valueOf(2)) == 0) {
    					System.out.println(1);
    				} else {
    					System.out.println(1);
    				}
    			} else {
    				if (num2[1].compareTo(BigInteger.valueOf(1)) == 0)
    					System.out.println(1);
    				else if (num2[1].compareTo(BigInteger.valueOf(2)) == 0) {
    					System.out.println(0);
    				} else {
    					System.out.println(0);
    				}
    			}
    		}
    	}
    }

<!-- /wp:code -->