题目描述：
HH 有一串由各种漂亮的贝壳组成的项链。HH 相信不同的贝壳会带来好运，所以每次散步完后，他都会随意取出一段贝壳，思考它们所表达的含义。HH 不断地收集新的贝壳，因此，他的项链变得越来越长。

有一天，他突然提出了一个问题：某一段贝壳中，包含了多少种不同的贝壳？这个问题很难回答...… 因为项链实在是太长了。于是，他只好求助睿智的你，来解决这个问题。
<!-- more -->


先以操作中的r排序一遍，然后遍历这个排序后的操作，在遍历的同时维护一颗线段树来记录答案并获取答案，输出，完成！



```cpp
// #pragma GCC optimize("Ofast", "inline", "-ffast-math")
// #pragma GCC target("avx,sse2,sse3,sse4,mmx")
#include<bits/stdc++.h>
#define ll long long
#define ull unsigned long long
#define N 1000010
#define mod 998244353
#define LINF 123456789123456789
#define INF 1234567890
#define abs(x) ((x)^((x)>>31))-((x) >> 31)
using namespace std;
ll n,m,x,y,z,t,k,cnt=1,ans[N];
ll a[N],b[N];
pair<pair<ll,ll> ,int> p[N];

ll tr[N<<2];
map<ll,ll> mp;
void init(int rt,int l,int r){
    if(l==r){
        tr[rt]=a[l];
        return ;
    }
    int mid = l+r>>1;
    init((rt<<1), l , mid);
    init((rt<<1|1),mid+1,r);
    tr[rt]=tr[rt<<1]+tr[(rt<<1|1)];
    return ;
}
ll get(int x,int y,int rt,int l,int r){
    if(x<=l and r<=y){
        return tr[rt];
    }
    ll mid = l+r>>1,ans=0;
    if(x<=mid)ans += get(x,y,(rt<<1),l,mid);
    if(y>mid)ans += get(x,y,(rt<<1|1),mid+1,r);
    return ans;
}
void add(int x,int y,int rt,int l,int r){
    if(l==r){
        tr[rt]+=y;
        return ;
    }
    int mid = l+r>>1;
    if(x<=mid)add(x,y,rt<<1,l,mid);
    else add(x,y,(rt<<1|1),mid+1,r);
    tr[rt]=tr[rt<<1]+tr[(rt<<1|1)];
    return ;
}

int main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    cin >> n;
    init(1,1,n);
    for(int i=1;i<=n;i++)cin >> a[i];
    cin >> k;
    for(int i=1;i<=k;i++)cin>>p[i].first.second >> p[i].first.first,p[i].second=i;
    sort(p+1,p+1+k);
    for(int i=1;i<=k;i++)
    {
        for(int j=cnt;j<=p[i].first.first;j++)
        {
            if(b[a[j]]) 
                add(b[a[j]],-1,1,1,n);
            add(j,1,1,1,n);
            b[a[j]]=j;
        }
        cnt=p[i].first.first+1;
        ans[p[i].second]=get(p[i].first.second,p[i].first.first,1,1,n);
    }
    for(int i=1;i<=k;i++){
        cout << ans[i] << "\n";
    }
    return 0;
}
```