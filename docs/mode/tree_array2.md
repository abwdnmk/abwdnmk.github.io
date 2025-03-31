# 树状数组2（差分）

前言可以看一下树状数组1；

上一个可以说是前缀和版本，而这一个就是差分版本了；

## 1.适合的问题

题目要求我们对某一个区间加上x，然后让我们求出经过操作后数组中某一个数的值的时候；

## 2.模板代码

题目链接<[P3368 【模板】树状数组 2 - 洛谷](https://www.luogu.com.cn/problem/P3368)>

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */\
#define ll long long
const int maxx=5e5+5;
ll a[maxx],tree[maxx];
int n,m;
int lowbit(int x){
	return x&(-x);
}
//利用差分思想 
void updata(int x,int y,int k){
	for(int i=x;i<=n;i+=lowbit(i)){
		tree[i]+=k;
	}
	for(int i=y+1;i<=n;i+=lowbit(i)){
		tree[i]-=k;
	}
}
//求出下标为x的数的值 
ll query(int x){
	ll sum=0;
	for(int i=x;i>=1;i-=lowbit(i)){
		sum+=tree[i];
	}
	return sum;
}
void solve() {
	cin>>n>>m;
	for(int i=1;i<=n;i++){
		cin>>a[i];
		updata(i,i,a[i]);
	}
	while(m--){
		int op;
		cin>>op;
		if(op==1){
			int x,y,k;
			cin>>x>>y>>k;
			updata(x,y,k);
		}
		else if(op==2){
			int x;
			cin>>x;
			ll ans=query(x);
			cout<<ans<<"\n";
		}
	}
}
signed main(int argc, char** argv) {
	ios :: sync_with_stdio(false);
	cin.tie(0), cout.tie(0);
	int t=1;
	//cin>>t;
	while(t--) {
		solve();
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)