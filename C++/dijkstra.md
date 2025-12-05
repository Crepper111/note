# dijkstra

> 单源最短路算法

- 不适合负权图

## 操作

- 蓝白点思想：白点代表已经找到最短路的点，蓝点代表还未找到最短路的点。同时白点的最短路肯定比蓝点近。
- 定义最短路数组d，初始时源点设为0，其他点设为最大值(inf)。一开始都有点都是蓝点
- 每次操作找出目前最短路d最小的蓝点x，将其变成白点，并用这个点“松弛”与之相连的其他蓝点，更新其他点的最短路（如下代码）。
```cpp
 if(d[x]+y.w<d[y.to]) d[y.to]=d[x]+y.w;
```
- 重复这个步骤，直到所有点都变成蓝点。

## 原理

- 本质其实是贪心。可以发现每次找到的蓝点x是距离源点最近的蓝点，且d[x]已经是最短路。
- 因为每次要找的最短点一定与白点直接相连（若最短点与白点之间还有中间点，那中间点显然比最短点要近），而所有与白点相邻的点都已被白点松弛，所以d最小的蓝点就是下一个白点。
- **注意**，此时其他与白点直接相连的蓝点的最短路不一定已被算出，因为在更近的蓝点变成白点后，他们可能会被这些点再次松弛，**只有最近的蓝点才不可能被松弛进而变成白点**。

## 优化

- 如果通过遍历所有点的方式寻找d值最小的x点，时间复杂度为$O(n^2)$。

- 可以考虑优先队列堆优化，我们知道新白点一定会在与目前白点直接相连的点中，所以每次加入白点进行松弛操作时，将被松弛的点加入优先队列中即可，总时间复杂度$O((n+m)log_2n)$。

## 代码

- 在进行松弛和变白点操作时，一定要记得先判断这个点是不是已经是白点了

[P4779 【模板】单源最短路径（标准版）](https://www.luogu.com.cn/problem/P4779)
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<vector>
#include<queue>
#define SET(a,b) memset(a,b,sizeof(a))
using namespace std;
int READ=0;int read(){if(READ){READ=0;return 0;}int readF=1,readK=0;char readC=getchar();while(readC<'0'||readC>'9'){if(readC=='-')readF=-1;readC=getchar();}while(readC>='0'&&readC<='9'){readK=readK*10+readC-'0';readC=getchar();}return readF*readK;} template<typename T,typename ...T2>
void read(T &RD,T2&...RD2){READ=1;int readF=1,readK=0;char readC=getchar();while(readC<'0'||readC>'9'){if(readC=='-')readF=-1;readC=getchar();}while(readC>='0'&&readC<='9'){readK=readK*10+readC-'0';readC=getchar();}RD=readF*readK;read(RD2...);}
int n,m,s;
const int N=1e5+10;
struct node
{
    int to,w;//to代表点，w在不同地方代表的意义不同
};
bool operator < (node x,node y)
{
    return x.w>y.w;
}//因为stl中的优先队列是大根堆，所以这里的运算符要反过来
vector<node>v[N];
int d[N],vis[N];
priority_queue<node>q;
int main()
{
    read(n,m,s);
    for(int i=1;i<=m;i++)
    {
        int x,y,w;
        read(x,y,w);
        v[x].push_back((node){y,w});
        //这里的w代表边权
    }
    SET(d,0x3f);
    d[s]=0;
    q.push((node){s,0});//先让源点变成白点，这里的w代表d数组的值
    while(q.size())
    {
        int x=q.top().to;
        q.pop();
        if(vis[x])continue;
        vis[x]=1;//变成白点
        for(auto y:v[x])
        {
            if(vis[y.to]) continue;
            if(d[x]+y.w<d[y.to])
            {
                d[y.to]=d[x]+y.w;
            }//松弛操作，这里的w代表边权
            q.push((node){y.to,d[y.to]});//入队，这里的w代表d数组值
        }
    }
    for(int i=1;i<=n;i++) printf("%d ",d[i]);
    return 0;
}
```
**The end**
