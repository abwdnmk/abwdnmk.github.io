# codeforces round 1015(div1+div2)

这场比赛差点连b题都没做出来，幸好有高人指点才做出来；

## A

题目链接<[Problem - A - Codeforces](https://codeforces.com/contest/2084/problem/A)>

应为要想一个数与i求模等于i-1那么就让这个数等于i-1是最好的；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	int n;
	cin>>n;
	if(n%2==0){
		cout<<"-1"<<"\n";
		return ;
	}
    cout<<n<<" ";
    for(int i=1;i<=n-1;i++){
    	cout<<i<<" ";
	}
	cout<<"\n";
}
//7
//1 2 3 4 5 6 7
//7 1 2 3 4 5 6
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

题目链接<[Problem - B - Codeforces](https://codeforces.com/contest/2084/problem/B)>

要想让最小的值成为一些数的最大公约数，那么这个值一定是数组里最小的值，然后将数组中这个最小值的倍数都取出来，然后求最大公约数，看是否相等即可；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	int n;
	cin>>n;
	vector<ll> v(n+1);
	for(int i=1;i<=n;i++){
		cin>>v[i];
	}
	sort(v.begin()+1,v.end());
	vector<ll> x;
	for(int i=2;i<=n;i++){
		if(v[i]%v[1]==0){
			x.push_back(v[i]);
		}
		if(v[i]==v[1]){
			cout<<"YES"<<"\n";
			return ;
		}
	}
	if(x.size()<=1){
		cout<<"NO"<<"\n";
		return ;
	}
	//6 8 12
    for(int i=1;i<x.size();i++){
    	x[i]=__gcd(x[i],x[i-1]);
	}
	for(int i=0;i<x.size();i++){
		if(v[1]==x[i]){
			cout<<"YES"<<"\n";
			return ;
		}
	}
	cout<<"NO"<<"\n";
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

## C

题目链接<[Problem - C - Codeforces](https://codeforces.com/contest/2084/problem/C)>

要想使对于每个个i等有a[i]==b[n-i+1],如果说存在a[i]==b[i]的情况，那么就只可能n是奇数的情况下才有可能，否则都不行，如果说有一个，那么就先排好这一个，然后再对i--n/2的每一个i排列一下就行，最后再判断，如果没有相等的，那么直接排列就行；

### 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve() {
	int n;
	cin>>n;
	vector<int> a(n+1),b(n+1);
	map<int,int> mp1,mp2;
	vector< pair<int,int> > v;
	for(int i=1; i<=n; i++) {
		cin>>a[i];
		mp1[a[i]]=i;
	}
	for(int i=1; i<=n; i++) {
		cin>>b[i];
		mp2[b[i]]=i;
	}
	int cnt=0;
	for(int i=1; i<=n; i++) {
		if(a[i]==b[i]) {
			cnt++;
		}
	}
	if(cnt>=2){
		cout<<"-1"<<"\n";
		return ;
	}
	if(cnt==1&&n%2==0){
		cout<<"-1"<<"\n";
		return ;
	}
	if(cnt!=1&&n%2==1){
		cout<<"-1"<<"\n";
		return ;
	}
	if(cnt==1){
		for(int i=1;i<=n;i++){
			if(a[i]==b[i]&&i!=n/2+1){
				if(i>n/2+1){
					v.push_back({n/2+1,i});
				}
				else{
					v.push_back({i,n/2+1});
				}
				swap(mp1[a[i]],mp1[a[n/2+1]]);
			    swap(mp2[b[i]],mp2[b[n/2+1]]);
			    swap(a[i],a[n/2+1]);
			    swap(b[i],b[n/2+1]);
			    break;
			}
		}
	}
	for(int i=1; i<=n/2; i++) {
		if(a[i]!=b[n-i+1]) {
			int x=mp2[a[i]];
			v.push_back({x,n-i+1});
			swap(mp1[a[x]],mp1[a[n-i+1]]);
			swap(mp2[b[x]],mp2[b[n-i+1]]);
			swap(a[x],a[n-i+1]);
			swap(b[x],b[n-i+1]);
		}
	}
	bool ok=false;
	for(int i=1;i<=n;i++){
		if(a[i]!=b[n-i+1]){
			ok=true;
			break;
		}
	}
	if(ok){
		cout<<"-1"<<"\n";
		return ;
	}
	cout<<v.size()<<"\n";
	for(int i=0;i<v.size();i++){
		cout<<v[i].first<<" "<<v[i].second<<"\n";
	}
}
signed main(int argc, char** argv) {
	ios :: sync_with_stdio(false);
	cin.tie(0), cout.tie(0);
	int t=1;
	cin>>t;
	while(t--) {
		solve();
	}
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
