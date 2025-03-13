# 关于单源最短路问题的dijstra算法模板

模板题目链接<[P4779 【模板】单源最短路径（标准版） - 洛谷](https://www.luogu.com.cn/problem/P4779)>

dijkstra算法主要是在有向图中求从一个点到其他点的最短路径；

看了题解之后还是不太理解，先保存着在慢慢看吧；

### 1.题解

具体思路：Dijkstra是基于一种贪心的策略，首先用数组dis记录起点到每个结点的最短路径，再用一个数组保存已经找到最短路径的点

然后，从dis数组选择最小值，则该值就是源点s到该值对应的顶点的最短路径，并且把该点记为已经找到最短路

此时完成一个顶点，再看这个点能否到达其它点（记为v），将dis[v]的值进行更新

不断重复上述动作，将所有的点都更新到最短路径

这种算法实际上是O(n^2)的时间复杂度，但我们发现在dis数组中选择最小值时，我们可以用一些数据结构来进行优化。~~线段树？平衡树？~~

其实我们可以用STL里的堆来进行优化，堆相对于线段树以及平衡树有着常数小，码量小等优点，并且堆的一个妙妙的性质就是可以在nlogn的时限内满足堆顶是堆内元素的最大（小）值，之不正是我们要的嘛？

### 2.代码

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
const int maxx=2e5+5;
const int N=1e5+5;
const ll INF=1e18;
int n,m,s;
vector< pair<int,int> > g[maxx];
bool vis[N];
ll dis[N];
void add_edge(int u,int v,int w){
	g[u].push_back({v,w});
}
priority_queue< pair<ll,int>, vector< pair<ll,int> >, greater< pair<ll,int> > > q;
void dijkstra(){
	q.push({0,1});
	while(!q.empty()){
		pair<ll,int> p=q.top();
		q.pop();
		int u=p.second;
		if(vis[u]) continue;
		vis[u]=true;
		for(int v=0;v<g[u].size();v++){
			int to=g[u][v].first,w=g[u][v].second;
			if(dis[to]>dis[u]+w){
				dis[to]=dis[u]+w;
				q.push({dis[to],to});
			}
		}
	}
	for(int i=1;i<=n;i++){
		cout<<dis[i]<<" ";
	}
}
int main(int argc, char** argv) {
	cin>>n>>m>>s;
	for(int i=1;i<=m;i++){
		int u,v,w;
		cin>>u>>v>>w;
		add_edge(u,v,w);
	}
	for(int i=1;i<=n;i++){
		dis[i]=INF;
	}
	dis[s]=0;
	dijkstra();
	return 0;
}
```
