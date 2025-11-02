# prim


[P3366 【模板】最小生成树](https://www.luogu.com.cn/problem/P3366)

```cpp
int vis[N];
int mst;
struct node
{
	int to,w;
};
bool operator < (node x,node y)
{
	return x.w>y.w;
}
priority_queue<node>q;
int tmp;
void prim()
{
	q.push((node){1,0});
	while(!q.empty())
	{
		int x=q.top().to;
		int w=q.top().w;
		q.pop();
		if(vis[x]) continue;
		vis[x]=1;
		tmp++;
		mst+=w;
		for(auto y:v[x])
		{
			int to=y.first;
			if(vis[to]) continue;
			q.push((node){to,y.second});
		}
	}
}
```