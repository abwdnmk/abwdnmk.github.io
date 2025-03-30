# codeforces round 1014 (div2)

## A

题目链接<[Problem - A - Codeforces](https://codeforces.com/contest/2092/problem/A)>

因为每个数加的d没有限制，所以最大的最大公约数就是最大的数减去最小的数；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	int n;
	cin>>n;
	vector<int> v(n+1,0);
	for(int i=1;i<=n;i++){
		cin>>v[i];
	}
	sort(v.begin()+1,v.end());
	int ans=v[n]-v[1];
	cout<<ans<<'\n';
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

题目链接<[Problem - B - Codeforces](https://codeforces.com/contest/2092/problem/B)>

阅读题意后我们发现在a中的下标为基数的字符只能由在b中下标为偶数的字符换过来，而在a中下标为偶数的字符也就只能由在b中下标为基数的字符得来，所以我们遍历a中1的个数以及相应的下标，遍历b中0的个数以及相应的下标，然后判断即可；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	int n;
	cin>>n;
	string a,b;
	cin>>a>>b;
	int cnt1=0,cnt2=0;
	for(int i=0;i<n;i++){
		if(i%2==0&&a[i]=='1'){
			cnt1++;
		}
		if(i%2==1&&a[i]=='1'){
			cnt2++;
		}
	}
	int cnt3=0,cnt4=0;
	for(int i=0;i<n;i++){
		if(i%2==1&&b[i]=='0'){
			cnt3++;
		}
		if(i%2==0&&b[i]=='0'){
			cnt4++;
		}
	}
	if(cnt1-cnt3<=0&&cnt2-cnt4<=0){
		cout<<"YES"<<endl;
		return ;
	}
	cout<<"NO"<<endl;
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

题目链接<[Problem - C - Codeforces](https://codeforces.com/contest/2092/problem/C)>

要想两个数加起来为奇数，就只能由一个奇数和一个偶数相加，观察发现，这样进行操作后，答案就一定是奇数，所以我们将输入的数按其奇偶性来区分，因为只有最大的奇数会改变，所以我们可以对其他的奇数与偶数中的0进行操作，奇数减一变偶数，所以最后的答案就是奇数的最大值加上所有的偶数和，再加上剩下的奇数和，再减去奇数的数量减一；

代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	int n;
	cin>>n;
	ll sumv=0,sumve=0;
	ll mx=0;
	vector<ll> v,ve;
	for(int i=1;i<=n;i++){
		ll num;
		cin>>num;
		if(num%2==1){
			v.push_back(num);
			sumv+=num;
		}
		else if(num%2==0){
			ve.push_back(num);
			sumve+=num;
		}
		mx=max(num,mx);
	} 
	sort(v.begin(),v.end());
	sort(ve.begin(),ve.end());
	if(v.size()==0||ve.size()==0){
		cout<<mx<<endl;
		return ;
	}
	int si=v.size(),sl=ve.size();
	ll ans=v[si-1]+sumve+sumv-v[si-1]-(si-1);
	cout<<ans<<endl;
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



