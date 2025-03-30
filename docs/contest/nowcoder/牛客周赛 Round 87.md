# 牛客周赛 Round 87

比赛链接<[(0条未读通知) 牛客竞赛_ACM/NOI/CSP/CCPC/ICPC算法编程高难度练习赛_牛客竞赛OJ](https://ac.nowcoder.com/acm/contest/105623)>

## A

题目链接<[A-小苯的V图_牛客周赛 Round 87](https://ac.nowcoder.com/acm/contest/105623/A)>

按照题目的意思去做就行

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */\
void solve(){
	int a1,a2,a3;
	cin>>a1>>a2>>a3;
	if(a1>a2&&a2<a3){
		cout<<"YES"<<endl;
		return ;
	}
	cout<<"NO"<<endl;
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

## B

题目链接<[B-小苯的数字切割_牛客周赛 Round 87](https://ac.nowcoder.com/acm/contest/105623/B)>

按照题意我们可以将这个数字变成字符串，然后暴力求解就行，n最大也就10的9次方，最多就是9*9的复杂度

### 代码：

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */\

void solve(){
	string s;
	cin>>s;
	s=" "+s;
    int n=s.size()-1;
    vector<int> sub(n+1),lis(n+1);
    for(int i=1;i<=n;i++){
    	int a=0,b=0;
    	for(int j=1;j<=i;j++){
    		a=a*10+(s[j]-'0');
		}
		sub[i]=a;
		for(int j=i+1;j<=n;j++){
			b=b*10+(s[j]-'0');
		}
		lis[i]=b;
	}
	int mx=0;
	for(int i=1;i<=n-1;i++){
		mx=max(mx,sub[i]+lis[i]);
	}
	cout<<mx<<"\n";
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

题目链接<[C-小苯的Z串匹配_牛客周赛 Round 87](https://ac.nowcoder.com/acm/contest/105623/C)>

按照题意可以想到先解决字符串中的<和>的取数问题是比较好的，然后再去解决Z的取值就行了；

### 代码：

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */\

void solve() {
	int n;
	cin>>n;
	vector<int> v(n+1);
	for(int i=1; i<=n; i++) {
		cin>>v[i];
	}
	string s;
	cin>>s;
	s=" "+s;
	int ans=0;
	for(int i=1; i<=n; i++) {
		if(s[i]=='<'&&v[i]>=0) {
			v[i]=-1;
			ans++;
		} else if(s[i]=='>'&&v[i]<=0) {
			v[i]=1;
			ans++;
		}
	}
	for(int i=2; i<=n; i++) {
		if(s[i]=='Z'&&v[i-1]<0&&v[i]>=0) {
			v[i]=-1;
			ans++;
		} else if(s[i]=='Z'&&v[i-1]>0&&v[i]<=0) {
			v[i]=1;
			ans++;
		}
	}
	cout<<ans<<"\n";
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

## D

题目链接<[D-小苯的最大和_牛客周赛 Round 87](https://ac.nowcoder.com/acm/contest/105623/D)>

刚开是以为是贪心，然后尝试使用双指针去解决这个问题，但是到后面问题越来越多，只要还是只有1个负数的时候去删除就很不好搞，赛时也没写出来，后来发现应该时dp，（那说到dp，这可是能和div2 b题坐一桌的题目了，属于是一生之敌了，难绷，放过我吧),就是应该考虑跳2个位置和3个位置就行；

### 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */\
#define ll long long
void solve() {
	int n;
	cin>>n;
	vector<ll> v(n+1);
	vector<ll> dp(n+1,0);
	for(int i=1;i<=n;i++){
	    cin>>v[i];
	}
	dp[0]=0;
	for(int i=1;i<=n;i++){
		dp[i]=dp[i-1]+v[i];
		if(i-2>=0) dp[i]=max(dp[i],dp[i-2]);
		if(i-3>=0) dp[i]=max(dp[i],dp[i-3]);
	}
	cout<<dp[n]<<"\n";
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

