# dp动态规划

这是一个关于wa学长不会AC动态规划的故事，我的动态规划绝对有问题；

## 1

题目链接<[1008 制衡](https://acm.hdu.edu.cn/contest/problem?cid=1153&pid=1008)>

题目应该时动态规划dp，我们可以想一下动态规划dp的每个下标的含义（虽然我根本不会，赛时也没写出来，唉。）

应为要进行段落的划分，那么对于dp[i] [j]而言，就代表在选择第i个数时，它位于第j段，使得这个求和尽可能的大，如果说我们知道了这个后就好搞了，那么遍历到第i个数的时候，只需要考虑，这个i是和第i-1个数处于一个段落，还是应该重启下一个段落。（还是不会写，感觉要哭了qwq）；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
void solve(){
	ll n,k;
	cin>>n>>k;
	ll dp[n+5][k+5],a[n+5][k+5];
	memset(dp,0,sizeof(dp));
	memset(a,0,sizeof(a));
	for(int i=1;i<=n;i++){
		for(int j=1;j<=k;j++){
			cin>>a[i][j];
		}
	}
	//dp[i][j]前面i被分了j段
	for(int i=1;i<=n;i++){
		for(int j=1;j<=k;j++){
			dp[i][j]=max(dp[i-1][j]+a[i][j],dp[i][j]);
			dp[i][j]=max(dp[i][j],dp[i][j-1]);
		}
	}
	cout<<dp[n][k]<<'\n';
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



## 2

题目链接<[1001 小凯逛超市](https://acm.hdu.edu.cn/contest/problem?cid=1154&pid=1001)>

刚看的时候觉得是完全背包，但是它和传统的完全背包不一样，它是求方案数，但后来发现，传统的完全背包是一维dp，这个应该是二维dp，dp的含义在代码中有；

### 代码

```cpp
#include <bits/stdc++.h> 
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
const int mod=1e9+7;
int dp[405][405];
//dp[i][j]表示使用不超过i的费用，购买不超过容量为j的物品的方案数
 
void solve(){
	int n,m,v;
	cin>>n>>m>>v;
	vector<int> a(n+1);
	for(int i=1;i<=n;i++){
		cin>>a[i];
	}
	memset(dp,0,sizeof(dp));
	dp[0][0]=1;
	for(int i=1;i<=n;i++){
		for(int j=a[i];j<=v;j++){
			for(int k=1;k<=m;k++){
				dp[j][k]=(dp[j][k]+dp[j-a[i]][k-1])%mod;
			}
		}
	}
	int ans=0;
	for(int i=0;i<=v;i++){
		ans=(ans+dp[i][m])%mod;
	}
	cout<<ans%mod<<"\n";
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

![点击并拖拽以移动]()

## 3

题目链接<[E-秘藏_牛客周赛 Round 88](https://ac.nowcoder.com/acm/contest/106318/E)>

这个只需要把状态处理好就行，考虑这个点可以怎么来就行，刚开始自己做才过了85%，唉，差点就以为自己是做动态规划的料了，要不是没有AC，我差点就信了；

### 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
/* run this program using the console pauser or add your own getch, system("pause") or input loop */
#define ll long long
const int maxx=2e5+10;
const int INF=-1e18;
ll dp[maxx][2];
//1代表在表世界，2代表在里世界
//那么dp[i][1]代表到达i点时且在表世界的最多金币
//dp[i][2]代表在i点且在里世界的最多金币 
void solve() {
	int n;
	ll k;
	cin>>n>>k;
	vector<ll> a(n+1),b(n+1);
	for(int i=1;i<=n;i++){
		cin>>a[i];
	} 
	for(int i=1;i<=n;i++){
		cin>>b[i];
	}
	for(int i=1;i<=n;i++){
		dp[i][1]=INF;
		dp[i][2]=INF;
	}
	dp[1][1]=a[1];
	//dp[0][1]=0,dp[0][2]=0;
	for(int i=2;i<=n;i++){
		dp[i][1]=max(dp[i][1],dp[i-1][1]+a[i]);
		if(dp[i-1][2]>=k){
			dp[i][1]=max(dp[i][1],dp[i-1][2]-k+a[i]);
		}
		dp[i][2]=max(dp[i][2],dp[i-1][2]+b[i]);
		if(dp[i-1][1]>=k){
			dp[i][2]=max(dp[i][2],dp[i-1][1]-k+b[i]);
		}
	}
	ll ans=max(dp[n][1],dp[n][2]);
	cout<<ans<<"\n";
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