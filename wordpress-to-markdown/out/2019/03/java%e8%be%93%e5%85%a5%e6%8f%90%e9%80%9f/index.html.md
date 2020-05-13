---
layout: post
title: JAVA输入提速
date: 2019-03-29
tags: ["基础__JAVA"]
---

<!-- wp:code -->

    内部类
    static class InputReader {
            public BufferedReader reader;
            public StringTokenizer tokenizer;

            public InputReader(InputStream stream) {
                reader = new BufferedReader(new InputStreamReader(stream), 32768);
                tokenizer = null;
            }

            public String next() {
                while (tokenizer == null '' !tokenizer.hasMoreTokens()) {
                    try {
                        tokenizer = new StringTokenizer(reader.readLine());
                    } catch (IOException e) {
                        throw new RuntimeException(e);
                    }
                }
                return tokenizer.nextToken();
            }

            public int nextInt() {
                return Integer.parseInt(next());
            }

        }

    第二个（复制于https://blog.csdn.net/lvlinfeng970/article/details/79922263）：

    import java.io.*;
    import java.util.*;
    import java.math.*;

    public class Main
    {

        public static void main(String[] args)
        {
            InputReader in = new InputReader();
            PrintWriter out = new PrintWriter(System.out);

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