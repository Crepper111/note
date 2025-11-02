# tarjan


[P3387 【模板】缩点](https://www.luogu.com.cn/problem/P3387)

```cpp
vector<int>v[N];
vector<int>o[N];
map<int,int>mp[N];
int dfn[N],low[N],cnt;
int st[N],top,vis[N];
int tag[N],c;
void tarjan(int x)
{
	dfn[x]=low[x]=++cnt;
	st[++top]=x;
	vis[x]=1;
	for(auto to:v[x])
	{
		if(!dfn[to])
		{
			tarjan(to);
			low[x]=min(low[x],low[to]);
		}
		else if(vis[to])
		{
			low[x]=min(low[x],dfn[to]);
		}
	}
	if(low[x]==dfn[x])
	{
		int j;c++;
		do
		{
			j=st[top--];
			vis[j]=0;
			tag[j]=c;
		}while(j!=x);
	}
}

for(int i=1;i<=n;i++)
		if(!dfn[i]) tarjan(i);
for(int i=1;i<=n;i++)
{
	for(auto to:v[i])
	{
		if(tag[i]==tag[to]) continue;
		if(mp[tag[i]].count(tag[to])) continue;
		o[tag[i]].push_back(tag[to]);
		mp[tag[i]][tag[to]]=1;
	}
}
```