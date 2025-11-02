# 倍增求LCA


[P3379 【模板】最近公共祖先（LCA）](https://www.luogu.com.cn/problem/P3379)

```cpp
void dfs(int x,int ft)
{
	dep[x]=dep[ft]+1;
	f[x][0]=ft;
	for(int i=1;i<=19;i++)
	{
		f[x][i]=f[f[x][i-1]][i-1];
	}
	for(auto to:v[x])
	{
		if(to==ft) continue;
		dfs(to,x);
	}
}
int lca(int x,int y)
{
	if(dep[x]<dep[y]) swap(x,y);
	for(int i=19;i>=0;i--)
	{
		if(dep[f[x][i]]>=dep[y]) x=f[x][i];
	}
	if(x==y) return x;
	for(int i=19;i>=0;i--)
	{
		if(f[x][i]!=f[y][i]) x=f[x][i],y=f[y][i];
	}
	return f[x][0];
}
```