---
layout: post
title: SDNUOJ-1000-1009
date: 2019-09-23
tags: ["OJ__SDNUOJ"]
---

<!-- wp:paragraph -->

自觉哦.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

1000:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int a,b;
        scanf("%d%d",&a,&b);
        {
            printf("%d\n",a+b);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1001:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int a,b;
        while(scanf("%d%d",&a,&b)!=EOF)
        {
            printf("%d\n",a+b);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1002:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int N;
        int a,b;
        int i=1;
        scanf("%d",&N);
        while(i<=N)
        {
            i++;
            scanf("%d%d",&a,&b);
            {
                printf("%d\n",a+b);
            }
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1003:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int a,b;
        while(scanf("%d%d",&a,&b)&&(a!=0&&b!=0))
        {
        printf("%d\n",a+b);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1004:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int N,i,sum,a;
        while(scanf("%d",&N)&&(N!=0))
        {
            sum=0;
            for(i=1;i<=N;i++)
            {
                scanf("%d",&a);
                sum+=a;
            }
            printf("%d\n",sum);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1005:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int N,sum;
        int a,b,c;
        int i;
        scanf("%d",&b);
        for(i=1;i<=b;i++)
        {
            scanf("%d",&N);
            sum=0;
            for(c=1;c<=N;c++)
            {
                scanf("%d",&a);
                sum+=a;
            }
            printf("%d\n",sum);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1006:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int N,i,sum,a;
        while(scanf("%d",&N)!=EOF)
        {
            sum=0;
            for(i=1;i<=N;i++)
            {
                scanf("%d",&a);
                sum+=a;
            }
            printf("%d\n",sum);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1007:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int a,b;
        while(scanf("%d%d",&a,&b)!=EOF)
        {
            printf("%d\n\n",a+b);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1008:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int N,sum;
        int a,b,c;
        int i;
        scanf("%d",&b);
        for(i=1;i<=b;i++)
        {
            scanf("%d",&N);
            sum=0;
            for(c=1;c<=N;c++)
            {
                scanf("%d",&a);
                sum+=a;
            }
            printf("%d\n\n",sum);
        }
        return 0;
    }

<!-- /wp:code -->

<!-- wp:paragraph -->

1009:

<!-- /wp:paragraph -->

<!-- wp:code -->

    #include<stdio.h>
    int main()
    {
        int n,m,i,a,sum;
        scanf("%d",&n);
        scanf("%d",&m);
        sum=0;
        for(i=1;i<=n;i++)
        {
            scanf("%d",&a);
            if(a>m)
            {
                sum=a+sum;
            }
        }
        printf("%d",sum);
        return 0;
    }

<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"></pre>
<!-- /wp:code -->