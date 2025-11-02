# dijkstra（堆优化）


[P4779 【模板】单源最短路径（标准版）](https://www.luogu.com.cn/problem/P4779)

```cpp
int d[N],v[N];
struct node
{
	int w,to;
};
priority_queue<node>q;
bool operator < (node x,node y)
{
	return x.w>y.w;
}
void dijkstra()
{
	d[s]=0;
	q.push((node){0,s});
	while(!q.empty())
	{
		int x=q.top().to;
		q.pop();
		if(v[x]) continue;
		v[x]=1;
		for(int i=lin[x];i;i=e[i].nxt)
		{
			int to=e[i].to;
			if(v[to]) continue;
			d[to]=min(d[to],d[x]+e[i].w);
			q.push((node){d[to],to});
		}
	}
}
```