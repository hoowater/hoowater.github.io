---
layout: page
title: "poj2187"
date: 2014-12-19 18:45
comments: true
sharing: true
footer: true
---
暴力代码
```c++
#include <iostream>
#include <cmath>
#include <cstdlib>
#include <cstdio>
#include <algorithm>
#include <cstring>
#define next (i+1)%n
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
    int x,y;
    Point() {}
    Point(int x,int y) : x(x),y(y) {}
    Point operator + (Point p)
    {
        return Point(x + p.x, y + p.y);    //向量 + 向量 = 向量
    }
    Point operator - (Point p)
    {
        return Point(x - p.x, y - p.y);    // 向量 - 向量 = 向量
    }
    bool operator < (const Point p) const
    {
        return x < p.x  || x == p.x && y < p.y;    //字典序比较，重定义<
    }
    bool operator == (const Point p) const
    {
        return x == p.x && y == p.y;    //重定义 ==
    }
    int dot(Point p)
    {
        return x * p.x + y * p.y;    //点积
    }
    int det(Point p)
    {
        return x * p.y - y * p.x;    //叉积,旋转方向取逆时针
    }
    int sqrlen()
    {
        return x*x + y*y;
    }
};

typedef Point Vector;
int u;
int ConvexHull(Point* p,int n, Point* ch)
{
    sort(p,p+n);
    int m = 0;
    for (int i = 0; i < n ; i ++)
    {
        while (m > 1 && (ch[m-1] - ch[m-2]).det(p[i] - ch[m-2]) <= 0) m --;
        ch[m++] = p[i];
    }
    int k = m;
    for (int i = n-2; i >= 0; i--)
    {
        while (m > k &&(ch[m-1] - ch[m-2]).det(p[i] - ch[m-2]) <= 0) m--;
        ch[m++] = p[i];
    }
    if (n > 1) m--;
    return m;
}

Point a[55555],Hull[100000];
int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
        scanf("%d%d", &a[i].x, &a[i].y);
    int m = ConvexHull(a, n, Hull);
    int ans = 0;
    for (int i = 0; i < m; i++)
        for (int j = i+1; j < m; j++)
            ans = max(ans, (Hull[i] - Hull[j]).sqrlen());
    printf("%d\n", ans);
    // system("pause");
    return 0;
}
```
旋转卡壳代码
```c++
#include <iostream>
#include <cmath>
#include <cstdlib>
#include <cstdio>
#include <algorithm>
#include <cstring>
#define next (i+1)%n
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
    int x,y;
    Point() {}
    Point(int x,int y) : x(x),y(y){}
    Point operator + (Point p) {return Point(x + p.x, y + p.y); }//向量 + 向量 = 向量
    Point operator - (Point p) {return Point(x - p.x, y - p.y); } // 向量 - 向量 = 向量
    bool operator < (const Point p) const {return x < p.x  || x == p.x && y < p.y; } //字典序比较，重定义<
    bool operator == (const Point p) const {return x == p.x && y == p.y; }//重定义 ==
    int dot(Point p) {return x * p.x + y * p.y; }//点积
    int det(Point p) {return x * p.y - y * p.x; }//叉积,旋转方向取逆时针
    int sqrDis(Point p){return (x - p.x)*(x - p.x) + (y - p.y)*(y - p.y);}
};
typedef Point Vector;
int u;
int ConvexHull(Point* p,int n, Point* ch)
{
    sort(p,p+n);
    int m = 0;
    for (int i = 0; i < n ; i ++)
    {
        while (m > 1 && (ch[m-1] - ch[m-2]).det(p[i] - ch[m-2]) <= 0) m --;
        ch[m++] = p[i];
    }
    int k = m;
    for (int i = n-2; i >= 0; i--)
    {
        while (m > k &&(ch[m-1] - ch[m-2]).det(p[i] - ch[m-2]) <= 0) m--;
        ch[m++] = p[i];
    }
    if (n > 1) m--;
    return m;
}

int Area(Point a, Point b, Point c)
{
  Vector v = b - a;
  return abs(v.det(c - a));
}

int RotatingCalipers(Point *ch, int n, int s)
{
  int q = s;
  int ans = ch[0].sqrDis(ch[s]);
  for (int i = 0; i < n; i ++)
  {
      while (Area(ch[i], ch[next], ch[(q+1)%n]) > Area(ch[i], ch[next], ch[q]))
          q = (q+1) % n;
      ans = max(ans,max(ch[i].sqrDis(ch[q]), ch[next].sqrDis(ch[(q+1)%n])));
  }
  return ans;
}
Point a[55555],Hull[100000];
int main()
{
  int n;
  scanf("%d", &n);
  for (int i = 0; i < n; i++)
      scanf("%d%d", &a[i].x, &a[i].y);
  int m = ConvexHull(a, n, Hull);
  int u = 0;
  for (int i = 1; i < m; i++)
      if (Hull[u].x < Hull[i].x || Hull[u].x == Hull[i].x && Hull[u].y < Hull[i].y)
          u = i;
  int ans = RotatingCalipers(Hull, m, u);
  printf("%d\n", ans);
  // system("pause");
  return 0;

```

[<--back](/blog/2014/12/19/2014bei-you-xin-sheng-xun-lian-4/)