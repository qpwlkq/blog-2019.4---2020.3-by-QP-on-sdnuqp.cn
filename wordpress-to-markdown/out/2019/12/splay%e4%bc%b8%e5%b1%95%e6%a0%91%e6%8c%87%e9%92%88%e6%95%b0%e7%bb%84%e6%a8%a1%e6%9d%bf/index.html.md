---
layout: post
title: splay伸展树指针+数组模板
date: 2019-12-05
tags: ["基础__STL"]
---

<!-- wp:code -->

    //#pragma GCC optimize("O3")
    //#include <bits/stdc++.h>
    //#define N 100005
    //#define inf 1000000005
    //using namespace std;
    //inline int read()
    //{
    //    register int x = 0, f = 1; register char ch = getchar();
    //    while (ch < '0' '' ch>'9') { if (ch == '-')f = -1; ch = getchar(); }
    //    while (ch >= '0' && ch <= '9')x = (x << 3) + (x << 1) + ch - '0', ch = getchar();
    //    return x * f;
    //}
    //inline void write(register int x)
    //{
    //    if (!x)putchar('0'); if (x < 0)x = -x, putchar('-');
    //    static int sta[36]; int tot = 0;
    //    while (x)sta[tot++] = x % 10, x /= 10;
    //    while (tot)putchar(sta[--tot] + 48);
    //}
    //struct node
    //{
    //    int v;
    //    int fa;
    //    int ch[2];
    //    int rec;
    //    int sum;
    //}tree[N];
    //int tot;
    //inline void update(register int x)
    //{
    //    tree[x].sum = tree[tree[x].ch[0]].sum + tree[tree[x].ch[1]].sum + tree[x].rec;
    //}
    //inline bool findd(register int x)
    //{
    //    return tree[tree[x].fa].ch[0] == x ? 0 : 1;
    //}
    //inline void connect(register int x, register int fa, register int son) //把x转为fa的son(son是0/1，表示左孩子或右孩子)
    //{
    //    tree[x].fa = fa;
    //    tree[fa].ch[son] = x;
    //}
    //inline void rotate(register int x)
    //{
    //    int Y = tree[x].fa;
    //    int R = tree[Y].fa;
    //    int Yson = findd(x);
    //    int Rson = findd(Y);
    //    int B = tree[x].ch[Yson ^ 1];
    //    connect(B, Y, Yson);
    //    connect(Y, x, Yson ^ 1);
    //    connect(x, R, Rson);
    //    update(Y), update(x);
    //}
    //inline void splay(register int x, register int to)
    //{
    //    to = tree[to].fa;
    //    while (tree[x].fa != to)
    //    {
    //        int y = tree[x].fa;
    //        if (tree[y].fa == to)
    //            rotate(x);
    //        else if (findd(x) == findd(y))
    //            rotate(y), rotate(x);
    //        else
    //            rotate(x), rotate(x);
    //    }
    //}
    //inline int newpoint(register int v, register int fa)
    //{
    //    tree[++tot].fa = fa;
    //    tree[tot].v = v;
    //    tree[tot].sum = tree[tot].rec = 1;
    //    return tot;
    //}
    //inline void Insert(register int x)
    //{
    //    int now = tree[0].ch[1];
    //    if (tree[0].ch[1] == 0)
    //    {
    //        newpoint(x, 0);
    //        tree[0].ch[1] = tot;
    //    }
    //    else
    //    {
    //        while (19260817)
    //        {
    //            ++tree[now].sum;
    //            if (tree[now].v == x)
    //            {
    //                ++tree[now].rec;
    //                splay(now, tree[0].ch[1]);
    //                return;
    //            }
    //            int nxt = x < tree[now].v ? 0 : 1;
    //            if (!tree[now].ch[nxt])
    //            {
    //                int p = newpoint(x, now);
    //                tree[now].ch[nxt] = p;
    //                splay(p, tree[0].ch[1]);
    //                return;
    //            }
    //            now = tree[now].ch[nxt];
    //        }
    //    }
    //}
    //inline int find(register int v)
    //{
    //    int now = tree[0].ch[1];
    //    while (19260817)
    //    {
    //        if (tree[now].v == v)
    //        {
    //            splay(now, tree[0].ch[1]);
    //            return now;
    //        }
    //        int nxt = v < tree[now].v ? 0 : 1;
    //        if (!tree[now].ch[nxt])
    //            return 0;
    //        now = tree[now].ch[nxt];
    //    }
    //}
    //inline void delet(register int x)
    //{
    //    int pos = find(x);
    //    if (!pos)
    //        return;
    //    if (tree[pos].rec > 1)
    //    {
    //        --tree[pos].rec;
    //        --tree[pos].sum;
    //    }
    //    else
    //    {
    //        if (!tree[pos].ch[0] && !tree[pos].ch[1])
    //            tree[0].ch[1] = 0;
    //        else if (!tree[pos].ch[0])
    //        {
    //            tree[0].ch[1] = tree[pos].ch[1];
    //            tree[tree[0].ch[1]].fa = 0;
    //        }
    //        else
    //        {
    //            int left = tree[pos].ch[0];
    //            while (tree[left].ch[1])
    //                left = tree[left].ch[1];
    //            splay(left, tree[pos].ch[0]);
    //            connect(tree[pos].ch[1], left, 1);
    //            connect(left, 0, 1);
    //            update(left);
    //        }
    //    }
    //}
    //inline int rank(register int v)
    //{
    //    int pos = find(v);
    //    return tree[tree[pos].ch[0]].sum + 1;
    //}
    //inline int arank(register int x)
    //{
    //    int now = tree[0].ch[1];
    //    while (19260817)
    //    {
    //        int used = tree[now].sum - tree[tree[now].ch[1]].sum;
    //        if (x > tree[tree[now].ch[0]].sum&& x <= used)
    //        {
    //            splay(now, tree[0].ch[1]);
    //            return tree[now].v;
    //        }
    //        if (x < used)
    //            now = tree[now].ch[0];
    //        else
    //            x -= used, now = tree[now].ch[1];
    //    }
    //}
    //inline int lower(register int v)
    //{
    //    int now = tree[0].ch[1];
    //    int ans = -inf;
    //    while (now)
    //    {
    //        if (tree[now].v<v && tree[now].v>ans)
    //            ans = tree[now].v;
    //        if (v > tree[now].v)
    //            now = tree[now].ch[1];
    //        else
    //            now = tree[now].ch[0];
    //    }
    //    return ans;
    //}
    //inline int upper(register int v)
    //{
    //    int now = tree[0].ch[1];
    //    int ans = inf;
    //    while (now)
    //    {
    //        if (tree[now].v > v&& tree[now].v < ans)
    //            ans = tree[now].v;
    //        if (v < tree[now].v)
    //            now = tree[now].ch[0];
    //        else
    //            now = tree[now].ch[1];
    //    }
    //    return ans;
    //}
    //int main()
    //{
    //    int m = read();
    //    while (m--)
    //    {
    //        int opt = read(), x = read();
    //        if (opt == 1)
    //            Insert(x);
    //        else if (opt == 2)
    //            delet(x);
    //        else if (opt == 3)
    //        {
    //            write(rank(x));
    //            printf("\n");
    //        }
    //        else if (opt == 4)
    //        {
    //            write(arank(x));
    //            printf("\n");
    //        }
    //        else if (opt == 5)
    //        {
    //            write(lower(x));
    //            printf("\n");
    //        }
    //        else
    //        {
    //            write(upper(x));
    //            printf("\n");
    //        }
    //    }
    //    return 0;
    //}

    #include <bits/stdc++.h>
    using namespace std;

    class spnode {
    public:
        spnode* l, * r, * f;
        int key;
        spnode(int k);
        void rightnode();
        void leftnode();
        static void splay(spnode* x, spnode* rt);
        spnode* find(int k);
        spnode* insert(int k);
        spnode* max();
        spnode* min();
        spnode* succ(int k);
        spnode* prev(int k);
        static spnode* join(spnode* x, spnode* y);
        static spnode* deletenode(spnode* x, spnode* y);
        static void split(int k, spnode* s, spnode*& x, spnode*& y);
    };

    spnode::spnode(int k) {
        key = k;
        l = r = f = NULL;
    }

    void spnode::rightnode() {
        spnode* y = f;
        f = y->f;
        if (f != NULL) {
            if (f->l == y)
                f->l = this;
            else
                f->r = this;
        }
        if (r != NULL)
            r->f = y;
        y->l = r;
        y->f = this;
        this->r = y;
    }

    void spnode::leftnode() {
        spnode* y = f;
        f = y->f;
        if (f != NULL) {
            if (f->l == y)
                f->l = this;
            else
                f->r = this;
        }
        if (l != NULL)
            l->f = y;
        y->r = l;
        y->f = this;
        this->l = y;
    }

    void spnode::splay(spnode *x, spnode *rt) {
        spnode* rtf = rt->f;
        while (x->f != rtf) {
            spnode* y = x->f;
            spnode* z = y->f;
            if (z == rtf) {
                if (y->l == x) x->rightnode();
                else x->leftnode();
            }
            else {
                if (y->l == x && z->l == y) {
                    y->rightnode();
                    x->rightnode();
                }
                else if (y->l == x && z->r == y) {
                    x->rightnode();
                    x->leftnode();
                }
                else if (y->r == x && z->l == y) {
                    x->leftnode();
                    x->rightnode();
                }
                else {
                    y->leftnode();
                    x->leftnode();
                }
            }
        }
    }

    spnode* spnode::find(int k) {
        if (k == key) return this;
        if (k < key) {
            if (l == NULL)
                return NULL;
            else
                l->find(k);
        }
        else {
            if (r == NULL)
                return NULL;
            else
                r->find(k);
        }
    }

    spnode* spnode::insert(int k) {
        if(k <= key) {
            if (l == NULL) {
                l = new spnode(k);
                l->f = this;
                return l;
            }
            else
                return l->insert(k);
        }
        else {
            if (r == NULL) {
                r = new spnode(k);
                r->f = this;
                return r;
            }
            else
                return r->insert(k);
        }
    }

    spnode* spnode::deletenode(spnode *x ,spnode *rt) {
        splay(x, rt);
        spnode* a = x->l;
        spnode* b = x->r;
        delete x;
        if (a != NULL) a->f = NULL;
        if (b != NULL) b->f = NULL;
        if (a == NULL) return b;
        if (b == NULL) return a;
        return join(a, b);
    }

    spnode* spnode::max() {
        if (r == NULL)
            return this;
        else
            r->max();
    }

    spnode* spnode::min() {
        if (l == NULL)
            return this;
        else
            l->min();
    }

    spnode* spnode::prev(int k) {
        if (key <= k) {
            if (r == NULL)
                return this;
            spnode* tmp = r->prev(k);
            if (tmp == NULL)
                return this;
            return tmp;
        }
        else {
            if (l == NULL)
                return NULL;
            return l->prev(k);
        }
    }

    spnode* spnode::succ(int k) {
        if (k <= key) {
            if (l == NULL)
                return this;
            spnode* tmp = l->succ(k);
            if (tmp == NULL)
                return this;
            return tmp;
        }
        else {
            if (r == NULL)
                return NULL;
            return r->succ(k);
        }
    }

    spnode* spnode::join(spnode *x ,spnode *y) {
        spnode* p = x->max();
        splay(p, x);
        p->r = y;
        y->f = p;
        return p;
    }

    void spnode::split(int k, spnode* s, spnode*& x, spnode*& y) {
        spnode* p = s->find(k);
        splay(p, s);
        x = p->l;
        y = p->r;
    } // 分离

    int main() {

        return 0;
    }

<!-- /wp:code -->