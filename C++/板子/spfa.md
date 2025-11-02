# SPFA
> 一个长度为4的算法

关于SPFA
- 它死了

[P3371 【模板】单源最短路径（弱化版）](https://www.luogu.com.cn/problem/P3371)

```cpp
int d[N],v[N];
queue<int>q;
void spfa()
{
	d[s]=0;
	q.push(s);
	v[s]=1;
	while(!q.empty())
	{
		int x=q.front();q.pop();
		v[x]=0;
		for(int i=lin[x];i;i=e[i].nxt)
		{
			int to=e[i].to;
			if(d[to]>d[x]+e[i].w)
			{
				d[to]=d[x]+e[i].w;
				if(!v[to]) q.push(to),v[to]=1;
			}
		}
	}
}
```