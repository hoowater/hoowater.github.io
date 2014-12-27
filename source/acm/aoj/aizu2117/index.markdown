---
layout: page
title: "Sourcer of Aizu2117"
date: 2014-12-19 18:46
comments: true
sharing: true
footer: true
---

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
#include <set>
#include <map>
#include <cmath>
using namespace std;
const double eps = 1e-9;
int dcmp(double x)//精度比&#36739;
{
    if (x < -eps) return -1;
    else if (x > eps) return 1;
    else return 0;
}


double add(double a, double b)//考&#34385;到精度的加法
{
    if (fabs(a + b) < eps * (fabs(a) + fabs(b))) return 0;
    return a + b;
}


struct Point//也可看做向量
{
    double x,y;
    Point() {}
    Point(double x,double y) : x(x),y(y){}
    Point operator + (Point p) {return Point(add(x, p.x),add(y, p.y)); }//向量 + 向量 = 向量
    Point operator - (Point p) {return Point(add(x, -p.x),add(y, -p.y)); } // 向量 - 向量 = 向量
    double length() {return sqrt(x*x + y*y); }//向量&#38271;度

};
struct Segment{
    Point a,b;
    void read(){
        scanf("%lf%lf%lf%lf", &a.x, &a.y, &b.x, &b.y);
    }
    double length(){return (a-b).length();}
};
Segment seg[18];
double dp[16][1<<14][2];
const int INF = 1e9;
int main()
{
/*    freopen("in.txt", "r", stdin);
    freopen("out.txt", "w", stdout);
*/    int n;
    int kase = 0;
    while (scanf("%d", &n) && n)
    {
        for (int i = 0; i < n; i++) seg[i].read();
        for (int i = 0; i < n; i++)
            for (int state = 1; state < (1<<n); state++)
                dp[i][state][0] = dp[i][state][1] = INF;
        double ans = 0;
        for (int i = 0; i < n; i++)
        {
            dp[i][1<<i][1] = dp[i][1<<i][0] = 0;
            ans += seg[i].length();
        }

        for (int state = 1; state < (1<<n); state++)
        {
            for (int j = 0; j < n; j++)
            {
                if ((state>>j)&1)
                    continue;
                for (int i = 0; i < n; i++)
                {
                    if((state>>i)&1)
                    {
                        dp[j][state|(1<<j)][0] = min(dp[j][state|(1<<j)][0],min(dp[i][state][0]+(seg[i].a-seg[j].b).length(), dp[i][state][1] + (seg[i].b - seg[j].b).length()));
                        dp[j][state|(1<<j)][1] = min(dp[j][state|(1<<j)][1],min(dp[i][state][0]+(seg[i].a-seg[j].a).length(), dp[i][state][1] + (seg[i].b - seg[j].a).length()));
                    }
                }
                /* printf("dp[%d][%d] = %.5f\n", i,state,min(dp[i][state][0],dp[i][state][1]));*/
            }
        }

        double addans = INF;
        for (int i = 0; i < n; i++)
            addans = min(addans,min(dp[i][(1<<n)-1][0],dp[i][(1<<n)-1][1]));
        printf("Case %d: %.5f\n", ++kase, ans+addans);
    }
}
```

[<--back](/blog/2014/12/19/2014bei-you-xin-sheng-xun-lian-4/)