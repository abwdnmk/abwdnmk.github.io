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
const int maxx=5e5+5;
const ll INF=0x3f3f3f3f;
int n,m,s,cnt=1;//cnt是add函数中用的； 
//n代表顶点数，m代表边的数量，s代表起点； 
int head[maxx],dis[maxx],vis[maxx];
//有向图中的边的存储； 
struct edge{
	int u,v,w,next;
}e[maxx];
priority_queue< pair<int,int> > q;
//有向图中边的添加,感觉不太适应这种方法啊，先用下面的吧； 
/*void add_edge(int u,int v,int w){
	e[cnt].u=u;
	e[cnt].v=v;
	e[cnt].w=w;
	
	e[cnt].next=head[u];
	head[u]=cnt;
	cnt++;
}*/
void dijkstra(){
	for(int i=1;i<=n;i++){
		dis[i]=INF;
	}
	dis[s]=0;
	q.push({0,s});
	while(!q.empty()){
		pair<int,int> p=q.top();
		q.pop();
		int u=p.second;
		if(vis[u]==1) continue;
		vis[u]=1;
		for(int i=head[u];i;i=e[i].next){
			int v=e[i].v;
			if(dis[v]>dis[u]+e[i].w){
				dis[v]=dis[u]+e[i].w;
				q.push({dis[v],v});
			}
		}
	}
}
int main(int argc, char** argv) {
	cin>>n>>m>>s;
	for(int i=1;i<=n;i++){
		cin>>e[i].u>>e[i].v>>e[i].w;
		e[i].next=head[e[i].u];
		head[e[i].u]=i;
	}
	dijkstra();
	for(int i=1;i<=n;i++){
		cout<<dis[i]<<" ";
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)