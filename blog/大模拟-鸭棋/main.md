没什么好说的，直接模拟！
<!-- more -->
上代码

```cpp
// #pragma GCC optimize("Ofast", "inline", "-ffast-math")
// #pragma GCC target("avx,sse2,sse3,sse4,mmx")
#include<bits/stdc++.h>
#define ll long long
#define ull unsigned long long
#define N 1000000
#define mod 998244353
#define LINF 123456789123456789
#define INF 1234567890
#define abs(x) ((x)^((x)>>31))-((x) >> 31)
using namespace std;
inline void swap(int &a,int &b){a=a^b;b=a^b;a=a^b;}inline void fopen(string s){freopen((s+".in").c_str(),"r",stdin),freopen((s+".out").c_str(),"w",stdout);}ll gcd(ll x,ll y){return x?y:gcd(x%y,y);}inline ll ksm(ll x,ll y){int z=1;while(y){if(y%2==1)z=z*x%mod;x=x*x%mod,y>>=1;}return z;}inline ll dd(ll x,ll y){return x*ksm(y,mod-2)%mod;}inline ll max(ll x,ll y){return x>y?x:y;}inline ll min(ll x,ll y){return x>y?y:x;}
ll n,m,x,y,z,t,k,ans,cnt,a,b;
//ll a[N],b[N],f[N];
//string s;
//register
// 代码：
string dz[] = {".","captain","guard","elephant","horse","car","duck","soldier"};  // 对照list
//                  王        士      象          马      车    鸭     兵
//             0    1         2       3           4       5     6      7
// 1:red  2:blue;
// 10*9
int rcx=0,rcy=4,bcx=9,bcy=4;  // 两个王的xy，用来方便'车'的将军判断

int f=1; // 己方color
bool flag=0;

int color[100][100] = {  //  红方还是蓝方
    {1,1,1,1,1,1,1,1,1},
    {0,0,0,0,0,0,0,0,0},
    {1,0,0,0,0,0,0,0,1},
    {1,0,1,0,1,0,1,0,1},
    {0,0,0,0,0,0,0,0,0},
    // 分割线
    {0,0,0,0,0,0,0,0,0},
    {2,0,2,0,2,0,2,0,2},
    {2,0,0,0,0,0,0,0,2},
    {0,0,0,0,0,0,0,0,0},
    {2,2,2,2,2,2,2,2,2},
};

int qp[100][100] = {   // 棋盘
    {5,4,3,2,1,2,3,4,5},
    {0,0,0,0,0,0,0,0,0},
    {6,0,0,0,0,0,0,0,6},
    {7,0,7,0,7,0,7,0,7},
    {0,0,0,0,0,0,0,0,0},
    // 分割线
    {0,0,0,0,0,0,0,0,0},
    {7,0,7,0,7,0,7,0,7},
    {6,0,0,0,0,0,0,0,6},
    {0,0,0,0,0,0,0,0,0},
    {5,4,3,2,1,2,3,4,5},
};

int M[4][2] = {1,-1,-1,1,1,1,-1,-1};

int MN[8][2] = {1,0,0,1,-1,0,0,-1,1,1,-1,-1,-1,1,1,-1};

bool bj;

// 是否符合规则：
bool check(int sx,int sy,int ex,int ey){
    bj=0;
    int s=qp[sx][sy];
    if(s==1){
        if(((ex==sx+1 or ex==sx-1) and ey==sy) or ((ey==sy+1 or ey==sy-1) and ex==sx))return 0;
        return 1;
    }if(s==2){
        if(((ex==sx+1 or ex==sx-1) and (ey==sy+1 or ey==sy-1))
         or ((ey==sy+1 or ey==sy-1) and (ex==sx+1 or ex==sx-1)))
            return 0;
        return 1;
    }if(s==3){
        for(int i=0;i<4;i++){
            int mx = M[i][0];
            int my = M[i][1];
            if(qp[sx+mx][sy+my]==0 and sx+mx*2==ex and sy+my*2==ey)return 0;
        }
        return 1;
    }if(s==4){
        for(int i=0;i<4;i++){
            int mx = M[i][1];
            int my = M[i][0];
            if(qp[sx+mx][sy]==0 and sx+mx*2==ex and sy+my*1==ey)return 0;
            if(qp[sx][sy+my]==0 and sx+mx*1==ex and sy+my*2==ey)return 0;
        }
        return 1;
    }if(s==5){
        if(sx!=ex and sy!=ey)return 1;
        if(sx==ex){
            for(int i=min(sy,ey)+1;i<max(sy,ey);i++){
                if(qp[sx][i])return 1;
            }
        }else{
            for(int i=min(sx,ex)+1;i<max(sx,ex);i++){
                if(qp[i][sy])return 1;
            }
        }
        return  0;
    }if(s==6){
        for(int i=0;i<4;i++){
            int mx = M[i][1];
            int my = M[i][0];
            if(!qp[sx+mx*2][sy+my] and !qp[sx+mx][sy] and ex==sx+mx*3 and ey==sy+my*2)return 0;
            if(!qp[sx+mx][sy+my*2] and !qp[sx][sy+my] and ex==sx+mx*2 and ey==sy+my*3)return 0;
        }
        return 1;
    }if(s==7){
        for(int i=0;i<8;i++){
            int mx = sx + MN[i][0];
            int my = sy + MN[i][1];
            if(ex==mx and ey==my)return 0;
        }
        return 1;
    }
    return 1;
}

bool jj(){ // 是否将军
    for(int i=0;i<10;i++){
        for(int j=0;j<9;j++){
            if(qp[i][j]==0)continue;
            if(color[i][j]==1){
                if(!check(i,j,bcx,bcy))return 1;
            }else{
                if(!check(i,j,rcx,rcy))return 1;
            }
        }
    }
    return 0;
}

bool win(){ // 是否获胜
    bool a,b;
    for(int i=0;i<10;i++)
        for(int j=0;j<9;j++){
            if(color[i][j]==1 and qp[i][j]==1)a=1;
            if(color[i][j]==2 and qp[i][j]==1)b=1;
        }
    if(!a or !b){
        flag=1;
    }
    return (a and b or !flag);
}

int main(){
    // ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    cin >> k;
    while(k--){
        cin >> x >> y >> a >> b;
// 不能将棋子移动到棋盘外的某个位置。
        if(x<0 or y<0 or a<0 or b<0 or x>=10 or a>=10 or y>=9 or b>=9)cout <<"Invalid command\n";
// 此步移动的初始位置无己方棋子停留。
        else if(!qp[x][y] or color[x][y]!=f)cout <<"Invalid command\n";
// 玩家不能将棋子移动到已经停留了己方棋子的位置。
        else if(color[x][y]==color[a][b])cout <<"Invalid command\n";
// 游戏已经结束。
        else if(flag)cout <<"Invalid command\n";
// 此步移动的初始位置有己方棋子停留，但移动不符合规则。
        else if(check(x,y,a,b))cout <<"Invalid command\n";
// 若合法,则输出：
        else {
            cout << (color[x][y]==1?"red ":"blue ") << (dz[qp[x][y]]) << ";";
            cout << (qp[a][b]?(color[a][b]==1?"red ":"blue ")+dz[qp[a][b]]:"NA") << ";";
            qp[a][b]=qp[x][y],color[a][b]=f,color[x][y]=0,qp[x][y]=0;
            if(qp[a][b]==1){
                if(color[a][b]==1)rcx=a,rcy=b;
                else bcx=a,bcy=b;
            }
            f=(f&1)+1;
            cout << (jj()?"yes":"no")<<";" << (win()?"no":"yes");
            cout << endl;
        }
    }
}

/*
错误条件：

* 不能将棋子移动到棋盘外的某个位置。
* 玩家不能将棋子移动到已经停留了己方棋子的位置。
* 此步移动的初始位置有己方棋子停留，但移动不符合规则。
* 此步移动的初始位置无己方棋子停留。
* 游戏已经结束。
*/
```