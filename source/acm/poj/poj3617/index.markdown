---
layout: page
title: "source of poj3617"
date: 2014-12-26 19:48
comments: true
sharing: true
footer: true
---
```c++
#include <iostream>
#include <cstring>
#include <cstdio>

using namespace std;

int main()
{
    char s1[10000],s2[10000],ans[10000];
    int n;
    cin>>n;
    int i=0;
    while (true)
    {
        char ch=getchar();
        if (ch>='A'&&ch<='Z')
        {
            s1[i++]=ch;
            s2[n-i]=ch;
        }
        if (i==n)
        {
            s1[i]=s2[i]='\0';
            break;
        }
    }
    i=0;
    int cnt1=0,cnt2=0;
    while (true)
    {
        if (strcmp(&s1[cnt1],&s2[cnt2])>0)
            ans[i++]=s2[cnt2++];
        else
            ans[i++]=s1[cnt1++];
        if (i==n)
        {
            ans[i]='\0';
            break;
        }
    }
    for (int i=0;i<strlen(ans);i++)
    {
        printf("%c",ans[i]);
        if ((i+1)%80==0) printf("\n");
    }
    printf("\n");
    return 0;
}
```
[<--BACK](/blog/2014/12/26/2014bei-you-xin-sheng-xun-lian-wu-div2ti-jie/)
