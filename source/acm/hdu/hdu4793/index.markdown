---
layout: page
title: "Source of hdu4793"
date: 2014-12-19 18:45
comments: true
sharing: true
footer: true
---
利用叉积的代码
```c++
#include <iostream>
#include <cmath>
#include <cstdlib>
#include <cstdio>
#include <algorithm>
#include <cstring>
#define next (i+1)%n

const double PI = acos(-1);
const double eps = 1e-10;
using namespace std;
int dcmp(double x)//精度比较
{
    if (x < -eps) return -1;
    else if (x > eps) return 1;
    else return 0;
}


double add(double a, double b)//考虑到精度的加法
{
    if (dcmp(a+b) == 0) return 0;
    return a + b;
}

struct Point//也可看做向量
{
    double x,y;
    Point() {}
    Point(int x,int y) : x(x),y(y) {}
    double length(){return sqrt(x*x + y*y);}
    double dot(Point p){return add(x*p.x, y*p.y);}
    double det(Point p){return add(x*p.y, -y*p.x);}
};

typedef Point Vector;


int main()
{
    double Rm,R,r,x,y,vx,vy;

    while (~scanf("%lf%lf%lf%lf%lf%lf%lf", &Rm, &R, &r, &x, &y, &vx, &vy))
    {
        Point p = Point(x, y);
        Vector v = Point(vx, vy);
        Vector v1 = Point(-x,-y);
        double speed = v.length();
        double dis = fabs(v1.det(v))/v.length();
        if (v.dot(v1) <= 0)//夹角大于90度，不可能进入圆内，时间为0；
            printf("0\n");
        else
        {
            if (dis >= R + r)
                printf("0\n");
            else if (dis >= Rm + r)
            {
                double d = 2*sqrt((R+r)*(R+r) - dis*dis);
                printf("%f\n", d/speed);
            }
            else
            {
                double d1 = sqrt((R+r)*(R+r) - dis*dis), d2 = sqrt((Rm+r)*(Rm+r) - dis*dis);
                double d = 2*(d1-d2);
                printf("%f\n", d/speed);
            }
        }
    }
}
```

利用距离公式的代码

```c++
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <cmath>
#include <algorithm>
#include <iostream>
#include <queue>
#define eps 1e-9
using namespace std;
typedef long long ll;
double rm, r, rr, x, y, vx, vy;
double v;

double ans;
void cal()
{
    double d = abs(y*vx-x*vy)/sqrt(vx*vx+vy*vy);
    if (d>=r+rr)
        ans = 0;
    else if ((d<r+rr)&&(d>rm+rr))
        ans = sqrt((r+rr)*(r+rr)-d*d)/v*2;
    else
        ans = (sqrt((r+rr)*(r+rr)-d*d)-sqrt((rm+rr)*(rm+rr)-d*d))/v*2;
}

int main()
{
    while (~scanf("%lf %lf %lf %lf %lf %lf %lf",  &rm, &r, &rr, &x, &y, &vx, &vy))
    {
        v = sqrt(vx*vx+vy*vy);
        if (-x*vx-y*vy<=eps)
            printf("%.3f\n", 0);
        else
        {
            cal();
            printf("%.3f\n", ans);
        }
    }
    return 0;

}
```

[<--back](/blog/2014/12/19/2014bei-you-xin-sheng-xun-lian-4/)