# 关于树的dfs模板的问题

其实好久之前就应该去把这个问题搞懂，但一直到现在，也是很难受了；

## 理解

其实树也是图的一种，感觉在绝大多数时候，树都被当做了一种没有环的无向图来使用，当然也不完全是这样，但这也导致树的构建方式和图的构建方式有很多相似的地方，也是很好了，下面是我自认为是树的dfs的模板，但可能根本不能直接去使用，肯定要变化的，但也有点用吧

粘贴一道题吧；

<[E-小红的陡峭值（四）_牛客周赛 Round 84](https://ac.nowcoder.com/acm/contest/103152/E)>

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
const int maxx=1e5+5;
//树的构造； 
vector<int> g[maxx];
//使用dfs遍历以f为父节点，u为子节点的的树；
//如果说是刚开始，那么f就是根节点，u为子节点； 
void dfs(int u,int f){
	//遍历当前节点u的所有邻接节点v； 
	for(int i=0;i<g[u].size();i++){
		int v=g[u][i];
		//如果v是u的父节点，则跳过； 
		if(v==f) continue;
		//递归调用dfs继续搜索以v为根的子树； 
		dfs(v,u);
	}
}
int main(int argc, char** argv) {
	int n;
	cin>>n;
	for(int i=1;i<=n-1;i++){
		int u,v;
		cin>>u>>v;
		g[u].push_back(v);
		g[v].push_back(u);
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)