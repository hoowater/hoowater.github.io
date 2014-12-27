---
layout: page
title: "soutce of hdu4813"
date: 2014-12-26 19:49
comments: true
sharing: true
footer: true
---
```c++
#include <cstdio>
#include <cstring>
#include <cstdlib>

int main()
{
    int l;
    scanf("%d", &l);
    while (l--)
    {
        int n,m;
        scanf("%d%d", &n, &m);
        char s[1005];
        scanf("%s", s);
        for (int i = 0; i < n; i++)
        {
            for (int j = i*m; j < i*m+m; j++)
                printf("%c", s[j]);
            printf("\n");
        }
    }
}
```

[<--BACK]()