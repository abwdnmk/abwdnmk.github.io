# educational codeforces round 177（div 2)

没想到我竟然战胜了传说中的div 2 的b题大人，这感觉真是太爽了，虽然说是侥幸而已，但还是有一定意义的，希望div 2大人以后也可以放我一马（放过我吧，不是故意要ac的）；

## A

题目链接<[Problem - A - Codeforces](https://codeforces.com/contest/2086/problem/A)>

其实这个题我题目都没读懂，单纯靠猜的，交了一发就对了，有点以外啊；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */

void solve(){
	 int n;
	 cin>>n;
	 cout<<n*2<<'\n';
}
signed main(int argc, char** argv) {
	ios :: sync_with_stdio(false);
	cin.tie(0), cout.tie(0);
	int t=1;
	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## B

题目链接<[Problem - B - Codeforces](https://codeforces.com/contest/2086/problem/B)>

感觉n和k两个数字都很大啊（看来一一枚举是无望了），但真的是这样吗。就一般来说吧，遇到这样的题目要么是复制存在一个上限，也就是说其他的都没有，要么就是只用看一到二个循环就行了，像这个题就是只用看一个就行了，从后往前遍历就行；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	 ll n,k,x;
	 cin>>n>>k>>x;
	 vector<ll> v(n+1);
	 ll sum=0;
	 for(int i=1;i<=n;i++){
	 	cin>>v[i];
	 	sum+=v[i];
	 }
	 if(sum*k<x){
	 	cout<<0<<"\n";
	 	return ;
	 }
	 ll p=x%sum,q=x/sum;
	 if(p==0){
	 	ll ans=n*k-q*n+1;
	 	cout<<ans<<"\n";
	 	return ;
	 }
	 ll sum1=0,j=0;
	 for(int i=n;i>=1;i--){
		 sum1+=v[i];
		 if(sum1>=p){
	 		j=i;
	 		break;
		 }
	 }
	 ll cn=n*(k-1)-q*n+j;
	 cout<<cn<<"\n";
}
//3 4 2 1 5  3 4 2 1 5   3 4 2 1 5
signed main(int argc, char** argv) {
	ios :: sync_with_stdio(false);
	cin.tie(0), cout.tie(0);
	int t=1;
	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## C

题目链接<[Problem - C - Codeforces](https://codeforces.com/contest/2086/problem/C)>

看来一下样例，感觉这个数组最后一定是变成1 2 3 4 …… n,所以感觉可以对每一个d[i]，我们可以去原数组中寻找这个数，并标记是否用过；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	 int n;
	 cin>>n;
	 vector<int> v(n+1),d(n+1),r(n+1);
	 for(int i=1;i<=n;i++){
	 	cin>>v[i];
	 	r[i]=i;
	 }
	 for(int i=1;i<=n;i++){
	 	cin>>d[i];
	 }
	 int ans=0;
	 for(int i=1;i<=n;i++){
	 	int x=v[d[i]];
	 	while(r[x]){
	 		ans++;
	 	    r[x]=0;
	 	    x=v[x];
		 }
		int y=d[i];
		while(r[y]){
			ans++;
			r[y]=0;
			y=v[y];
		}
		cout<<ans<<" ";
	 }
	 cout<<"\n";
}
//本题按道理来说，最后的序列应该是1 2 3 -- n这个样子
//我们应该记录每一个数字i是否被用过 
signed main(int argc, char** argv) {
	ios :: sync_with_stdio(false);
	cin.tie(0), cout.tie(0);
	int t=1;
	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

