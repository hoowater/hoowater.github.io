---
layout: page
title: "source of poj1088"
date: 2014-12-26 19:48
comments: true
sharing: true
footer: true
---

记忆化搜索

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
#include <cmath>

using namespace std;
int dd[4][2]={ {0,1}, {1,0}, {0,-1}, {-1,0} };
int h[110][110];
int dp[110][110];
int R,C;
int ans = 0;
int dfs(int x, int y)
{
    if (dp[x][y] > 1) return dp[x][y];
    for (int i = 0; i <= 3; i++)
    {
        int nextx = x+dd[i][0], nexty = y+dd[i][1];
        if (nextx >= 1 && nextx <= R && nexty >= 1 && nexty <= C)
            if (h[x][y] < h[nextx][nexty])
                dp[x][y] = max(dp[x][y], dfs(nextx, nexty)+1);
    }
    ans = max(ans, dp[x][y]);
    return dp[x][y];

}
int main()
{
    scanf("%d%d", &R, &C);

    for (int i = 1; i <= R; i++)
        for (int j = 1; j <= C; j++)
        {
            scanf("%d", &h[i][j]);
            dp[i][j] = 1;
        }

    ans = 0;
    for (int i = 1; i <= R; i++)
        for (int j = 1; j <= C; j++)
            if (dp[i][j] == 1)
               dp[i][j] = dfs(i,j);

    printf("%d\n", ans);
    return 0;
}

```

dp方法:

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>
#include <cmath>

using namespace std;

struct data
{
    int x,y,h;
    data(){}
    data(int x, int y, int h):x(x),y(y),h(h){}
    bool operator<(const data b)const{return h<b.h;}
}rec[11000];
int dd[4][2]={ {0,1}, {1,0}, {0,-1}, {-1,0} };
int h[110][110];
int dp[110][110];
int R,C;

int main()
{
    scanf("%d%d", &R, &C);
    int cnt = 0;
    for (int i = 1; i <= R; i++)
        for (int j = 1; j <= C; j++)
        {
            scanf("%d", &h[i][j]);
            rec[cnt++] = data(i,j,h[i][j]);
            dp[i][j] = 1;
        }
    sort(rec, rec+cnt);
    int ans = 0;
    for (int t = 0; t < cnt; t++)
    {
        int i = rec[t].x, j = rec[t].y;
        for (int k = 0; k < 4; k++)
        {
            int nexti = i+dd[k][0], nextj = j+dd[k][1];
            if (nexti >= 1 && nexti <= R && nextj >= 1 && nextj <= C)
                if (h[i][j] > h[nexti][nextj])
                    dp[i][j] = max(dp[i][j], dp[nexti][nextj]+1);
        }
        ans= max(ans, dp[i][j]);
    }

    printf("%d\n", ans);
    return 0;
}

```

[<--BACK](/blog/2014/12/26/2014bei-you-xin-sheng-xun-lian-wu-div2ti-jie/)
