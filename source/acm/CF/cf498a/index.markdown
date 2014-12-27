---
layout: page
title: "source of cf498a"
date: 2014-12-26 19:49
comments: true
sharing: true
footer: true
---
```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
#include <cmath>

int main()
{
    double x1,y1,x2,y2;
    scanf("%lf%lf", &x1, &y1);
    scanf("%lf%lf", &x2, &y2);
    int n;
    scanf("%d", &n);
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        int a,b,c;
        scanf("%d%d%d", &a, &b, &c);
        if ((a*x1+b*y1+c)*(a*x2+b*y2+c) < 0)
            ans++;
    }
    printf("%d\n", ans);
}
```
[<--BACK](/blog/2014/12/26/2014bei-you-xin-sheng-xun-lian-wu-div2ti-jie/)