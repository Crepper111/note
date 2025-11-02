# floyed

[【模板】单源最短路径（弱化版）](https://www.luogu.com.cn/problem/P3371) 40pts

```cpp
SET(d,0x3f);
for(int i=1;i<=n;i++) d[i][i]=0;
for(int i=1;i<=m;i++)
{
	int u,v,w;
	read(u,v,w);
	d[u][v]=min(d[u][v],w);
}
for(int k=1;k<=n;k++)
{
	for(int i=1;i<=n;i++)
	{
		for(int j=1;j<=n;j++)
		{
			d[i][j]=min(d[i][j],d[i][k]+d[k][j]);
		}
	}
}
```