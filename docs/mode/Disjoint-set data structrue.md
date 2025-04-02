# 并查集

并查集可以用来合并连通块以及查询两个点是否是属于一个祖先。

常用的可以用来判断一个图是否有环，或者是确定需要建立多少条线段可以把所有的点链接起来，也就是说是检查图的连通性；

## 1.检查图的联通性

题目链接<[P1111 修复公路 - 洛谷](https://www.luogu.com.cn/problem/P1111)>

像这种题目就是要求我们将所有的点连接起来，也就是将这n个点连通，不过本题还要对时间进行排序，以求找到最短时间。

### 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
const int maxx=1e3+5;
const int N=1e5+5;
int f[maxx];
struct node{
	int x,y,t;
}a[N];
int fm(node p,node q){
	return p.t<q.t;
}
int find(int x){
	return f[x]==x?x:(f[x]=find(f[x]));
}
void solve(){
	int n,m;
	cin>>n>>m;
	for(int i=1;i<=n;i++){
		f[i]=i;
	}
	for(int i=1;i<=m;i++){
		cin>>a[i].x>>a[i].y>>a[i].t;
	}
	sort(a+1,a+m+1,fm);
	for(int i=1;i<=m;i++){
		int fx=find(a[i].x),fy=find(a[i].y);
		if(fx!=fy) f[fx]=fy,n--;
		if(n==1){
			cout<<a[i].t<<endl;
			return ;
		}
	}
	cout<<"-1"<<endl;
}
int main(int argc, char** argv) {
	int t=1;
	//cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.检查图中是否有环

题目链接<[C - Make it Forest](https://atcoder.jp/contests/abc399/tasks/abc399_c)>

这个题目就是要求我们把图变成森林,也就是说要把图中的环给断掉，

所以我们在添加边的时候就可以判断这两个点的祖先是否一致，如果是一致的，那么就删除掉，不然就会成环。

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
const int maxx=2e5+5;
int f[maxx];
int find(int x){
	return f[x]==x?x:f[x]=find(f[x]);
}
void solve(){
	int n,m;
	cin>>n>>m;
	for(int i=1;i<=n;i++){
		f[i]=i;
	}
	int ans=0;
	for(int i=1;i<=m;i++){
		int u,v;
		cin>>u>>v;
		int x=find(u),y=find(v);
		if(x==y){
			ans++;
			continue;
		}
		f[y]=x;
	}
	cout<<ans<<"\n";
}
signed main(int argc, char** argv) {
	ios :: sync_with_stdio(false);
	cin.tie(0), cout.tie(0);
	int t=1;
	//cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

