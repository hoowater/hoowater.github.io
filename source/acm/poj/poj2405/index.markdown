---
layout: page
title: "poj2405"
date: 2014-12-19 18:46
comments: true
sharing: true
footer: true
---

```c++
#include <cstdio>
#include <cstring>
#include <cstdlib>
#include <cmath>
#include <iostream>

const double PI = acos(-1);

int main()
{
    int D,V;
    while (scanf("%d%d", &D, &V) == 2)
    {
        if (D == 0 && V == 0)
            break;
        double d = pow(D*D*D - 6.0/PI*V, 1.0/3);
        printf("%.3f\n", d);
    }
    return 0;

}
```

[<--back](/blog/2014/12/19/2014bei-you-xin-sheng-xun-lian-4/)