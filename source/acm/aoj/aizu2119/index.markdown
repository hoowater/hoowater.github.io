---
layout: page
title: "Source of aizu2119"
date: 2014-12-19 18:45
comments: true
sharing: true
footer: true
---
```c++
#include <cstring>
#include <cstdlib>
#include <cstdio>
#include <cmath>
#include <iostream>

int a[22];
using namespace std;
int solve(int n, int m)
{
    memset(a, 0, sizeof(a));
    int cnt = 0;
    int rec = 0;
    a[0] = n;
    while (a[m] == 0)
    {
        int cnt0 = 0;
        for (int i = rec; i >= 0; i--)
        {
            int tmp = a[i] / 2;
            a[i+1] += tmp;
            cnt0 += tmp;
            a[i] -= 2*tmp;
        }
        a[0] += cnt0;
        if (a[rec+1])
            rec++;
        cnt++;
    }
    return cnt;
}
int main()
{
    int n,m;
    int kase = 0;
    while (scanf("%d%d", &n, &m))
    {
        if (n == 0 && m == 0)
            break;
        printf("Case %d: %d\n", ++kase, solve(n,m));
    }
    return 0;
}
```

[<--back](/blog/2014/12/19/2014bei-you-xin-sheng-xun-lian-4/)