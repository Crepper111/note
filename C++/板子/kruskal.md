# kruskal


[P3366 【模板】最小生成树](https://www.luogu.com.cn/problem/P3366)

```cpp
struct edge
{
	int x,y,w;
}e[M];
bool operator < (edge x,edge y)
{
	return x.w<y.w;
}
int fa[N];
int find(int x)
{
	if(fa[x]==x) return x;
	return fa[x]=find(fa[x]);
}
int mst;
void kruskal()
{
	sort(e+1,e+m+1);
	for(int i=1;i<=n;i++) fa[i]=i;
	for(int i=1;i<=m;i++)
	{
		if(find(e[i].x)!=find(e[i].y))
		{
			fa[find(e[i].x)]=find(e[i].y);
			mst+=e[i].w;
		}
	}
}
```

# kruskal重构树


[P2245 星际导航](https://www.luogu.com.cn/problem/P2245)

```cpp
vector<int>v[N*2];
int a[N*2],cnt;
struct edge
{
	int x,y,w;
}e[M];
bool operator < (edge x,edge y)
{
	return x.w<y.w;
}
int fa[N*2];
int find(int x)
{
	if(fa[x]==x) return x;
	return fa[x]=find(fa[x]);
}
void kruskal()
{
	sort(e+1,e+m+1);
	for(int i=1;i<=n;i++) fa[i]=i;
	cnt=n;
	for(int i=1;i<=m;i++)
	{
		int fx=find(e[i].x),fy=find(e[i].y);
		if(fx!=fy)
		{
			fa[fx]=fa[fy]=++cnt;
			fa[cnt]=cnt;
			v[cnt].push_back(fx);
			v[cnt].push_back(fy);
			a[cnt]=e[i].w;
		}
	}
}
int dep[N*2];
int fz[N*2][19];
void dfs(int x,int ft)
{
	dep[x]=dep[ft]+1;
	fz[x][0]=ft;
	for(int i=1;i<=18;i++)
	{
		fz[x][i]=fz[fz[x][i-1]][i-1];
	}
	for(auto to:v[x])
	{
		if(to==fz[x][0]) continue;
		dfs(to,x);
	}
}
int lca(int x,int y)
{
	if(dep[x]<dep[y]) swap(x,y);
	for(int i=18;i>=0;i--)
	{
		if(dep[fz[x][i]]>=dep[y]) x=fz[x][i];
	}
	if(x==y) return x;
	for(int i=18;i>=0;i--)
	{
		if(fz[x][i]!=fz[y][i]) x=fz[x][i],y=fz[y][i];
	}
	return fz[x][0];
}
```