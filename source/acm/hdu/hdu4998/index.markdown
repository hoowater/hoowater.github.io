---
layout: page
title: "hdu4998"
date: 2014-12-19 18:46
comments: true
sharing: true
footer: true
---
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
    Point(double x,double y) : x(x),y(y) {}
    Point operator-(Point p){return Point(add(x, -p.x), add(y, -p.y));}
    Point operator+(Point p){return Point(add(x, p.x), add(y, p.y));}
    Point operator*(double t){return Point(x*t, y*t);}
    double length(){return sqrt(x*x + y*y);}
    double Angle(){return atan2(y, x);}
    double dot(Point p){return add(x*p.x, y*p.y);}
    double det(Point p){return add(x*p.y, -y*p.x);}//叉积
    Point Rotate(double rad){return Point(add(x*cos(rad), -y*sin(rad)), add(x*sin(rad), y*cos(rad)));}
    Point Normal(){return Point(-y, x);}//就直接求法向量了
};

typedef Point Vector;

Point GetLineIntersection(Point P, Vector v, Point Q, Vector w)
{
    Vector u = P - Q;
    return P + v*(w.det(u) / v.det(w));
}


int main()
{
    int T;
    cin>>T;
    while (T--)
    {
        int n;
        scanf("%d", &n);
        Point p1 = Point(55,78), q1 = Point(-86, 36);
        Point p2 = p1, q2 = q1;
        for (int i = 0; i < n; i++)
        {
            Point o;
            double rad;
            scanf("%lf%lf%lf", &o.x, &o.y, &rad);
            p2 = o + (p2-o).Rotate(rad);
            q2 = o + (q2-o).Rotate(rad);
           // printf("%f %f\n", p2.x, p2.y);
        }
        Point ansp = GetLineIntersection((p1+p2)*0.5, (p1-p2).Normal(), (q1+q2)*0.5, (q1-q2).Normal());
        double ansrad = (p2 - ansp).Angle() - (p1 - ansp).Angle();
        while (ansrad < 0) ansrad += 2*PI;
        while (ansrad > 2*PI) ansrad -= 2*PI;
        printf("%f %f %f\n", ansp.x, ansp.y, ansrad);

    }
}
```

[<--back](/blog/2014/12/19/2014bei-you-xin-sheng-xun-lian-4/)
