# 树状数组1（对单点增加值）

树状数组不同于前缀和，不同的点在于前缀和的维护的复杂度是O(n)，而树状数组的维护只需要log(n)，复杂度可谓是大大减小，所以当遇到使用前缀和无法解决的问题时，可以考虑一下树状数组；

## 1.适合的问题

当问题只是要求我们对数组中的一个值进行改变，然后要求我们求出改变后的数组中某一个区间的每一个数的和的时候，就可以考虑树状数组；

## 2.模板代码

模板链接<[P3374 【模板】树状数组 1 - 洛谷](https://www.luogu.com.cn/problem/P3374)>

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */\
const int maxx=5e5+5;
int n,m;
//数组a为原数组，tree为树状数组 
int a[maxx],tree[maxx];
//树状数组所应用的遍历方式 
int lowbit(int x){
	return x&(-x);
}
//更新操作 
void updata(int x,int y){
	for(int i=x;i<=n;i+=lowbit(i)){
		tree[i]+=y;
	}
}
//查询从1到下标x的和 
int query(int x){
	int sum=0;
	for(int i=x;i>=1;i-=lowbit(i)){
		sum+=tree[i];
	}
	return sum;
}
void solve(){
	memset(tree,0,sizeof(tree));
	cin>>n>>m;
	for(int i=1;i<=n;i++){
		cin>>a[i];
		updata(i,a[i]);
	}
	while(m--){
		int op,x,y;
		cin>>op>>x>>y;
		if(op==1){
			updata(x,y);
		}
		else if(op==2){
			int ans=query(y)-query(x-1);
			cout<<ans<<"\n";
		}
	}
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