# 整数在模p下的乘法逆元

在遇到a/b%p问题时，如果说b是一个很大的数，就要用到逆元了；

在乘法中，当一个数a，对于a*x%p=1，那么x就是a在模p下的乘法逆元了，那么上述式子就可以变为求b在mod p下的逆元，然后乘上a后mod p的值；

在求逆元时，有线性公式可以使用，就时ans[1]=1,ans[i]=(p-p/i)*ans[p%i]%p;根据之前的逆元求出当前元素的逆元；

## 代码

```cpp
#define ll long long
const int maxx=3e6+5;
ll ans[maxx];
void solve(){
    ll n,p;
    cin>>n>>p;
    ans[1]=1;
    cout<<ans[1]<<"\n";
    for(int i=2;i<=n;i++){
        ans[i]=(p-p/i)*ans[p%i]%p;
        //由前面的逆元快速求当前的逆元
        cout<<ans[i]<<"\n";
    }
}
// 相当于给了我们一个数a,让我们找到另外的一个数x，使得a*x%p==1；
// 这样的话，x就是a在模p下的乘法逆元
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

粘贴一道题目便于理解<[B3717 组合数问题 - 洛谷](https://www.luogu.com.cn/problem/B3717)>