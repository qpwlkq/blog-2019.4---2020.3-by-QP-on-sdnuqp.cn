---
layout: post
title: ZOJ-4107-Singing Everywhere-BY Java
date: 2019-05-05
tags: ["基础__JAVA","题解"]
---

<!-- wp:paragraph -->

题目本身是一个模拟，水题，但我脑抽用了Java，正常输入输出超时，还要加上输入输出挂。

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

AC code：

<!-- /wp:paragraph -->

<!-- wp:code -->

    import java.io.*;
    import java.math.*;
    import java.util.*;

    public class Main {

    	public static void main(String[] args) {
    //		Scanner in = new Scanner(new BufferedInputStream(System.in));
    		InputReader in = new InputReader();
            PrintWriter out = new PrintWriter(System.out);
    		int t = in.nextInt();
    		int n;
    		int sum, maxx;/*0/1/2*/
    		int[] a = new int[100010];
    		while (t-- >= 1) {
    			sum = 0;
    			n = in.nextInt();
    			for (int i = 1; i <= n; i++) {
    				a[i] = in.nextInt();
    			}
    			if (n == 1 '' n == 2 '' n == 3) {
    				System.out.println(0);
    				continue;
    			}
    			for (int i = 2; i <= n-1; i++) {
    				if (a[i - 1] < a[i] && a[i] > a[i + 1]) {
    					sum++;
    				}
    			}
    			if (sum == 0) {
    				System.out.println(0);
    				continue;
    			}
    //			System.out.println(sum);
    			maxx = 0;
    			if (a[1] < a[2] && a[2] > a[3]) {
    				maxx = 1;
    			} else if (a[n - 2] < a[n - 1] && a[n - 1] > a[n]) {
    				maxx = 1;
    			} else {
    				;
    			}
    			for (int i = 2; i <= n - 1; i++) {
    				if (a[i - 1] < a[i] && a[i] > a[i + 1]) {
    					if (a[i - 1] != a[i + 1]) {
    						if (i >= 3) {
    							if (a[i - 1] > a[i + 1] && a[i - 2] >= a[i - 1]) {
    								maxx = Math.max(maxx, 1);
    							}
    						} else if (i >= n - 2) {
    							if (a[i - 1] < a[i + 1] && a[i + 1] <= a[i + 2]) {
    								maxx = Math.max(maxx, 1);
    							}
    						}
    					}
    				} else if (i >= 3 && i <= n - 2) {
    					if (a[i - 2] < a[i - 1] && a[i - 1] > a[i] && a[i] < a[i + 1] & a[i + 1] > a[i + 2]) {
    						if (a[i - 1] == a[i + 1])
    							maxx = 2;
    						else
    							maxx = Math.max(maxx, 1);
    					}
    				}
    			}
    //			System.out.println(maxx);
    			System.out.println(sum - maxx);
    		}
            out.close();
    	}
    }

    class InputReader
    {
        BufferedReader buf;
        StringTokenizer tok;
        InputReader()
        {
            buf = new BufferedReader(new InputStreamReader(System.in));
        }
        boolean hasNext()
        {
            while(tok == null '' !tok.hasMoreElements()) 
            {
                try
                {
                    tok = new StringTokenizer(buf.readLine());
                } 
                catch(Exception e) 
                {
                    return false;
                }
            }
            return true;
        }
        String next()
        {
            if(hasNext()) return tok.nextToken();
            return null;
        }
        int nextInt()
        {
            return Integer.parseInt(next());
        }
        long nextLong()
        {
            return Long.parseLong(next());
        }
        double nextDouble()
        {
            return Double.parseDouble(next());
        }
        BigInteger nextBigInteger()
        {
            return new BigInteger(next());
        }
        BigDecimal nextBigDecimal()
        {
            return new BigDecimal(next());
        }
    }

<!-- /wp:code -->