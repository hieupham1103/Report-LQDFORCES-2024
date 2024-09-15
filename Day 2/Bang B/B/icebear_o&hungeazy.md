# Code gốc
<table>
<tr>
    <th>hungeazy</th>
    <th>icebear_o</th>
</tr>
<tr>
<td>
  
```cpp
/*
* @Author: hungeazy
* @Date:   2024-09-15 19:33:37
* @Last Modified by:   hungeazy
* @Last Modified time: 2024-09-15 19:37:05
*/
#include <bits/stdc++.h>
// #pragma GCC optimize("O3")  
// #pragma GCC optimize("unroll-loops")  
// #pragma GCC target("avx2,bmi,bmi2,popcnt,lzcnt")  
using namespace std;
#define fast ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL);
#define int long long
#define ull unsigned long long
#define sz(x) x.size()
#define sqr(x) (1LL * (x) * (x))
#define all(x) x.begin(), x.end()
#define fill(f,x) memset(f,x,sizeof(f))
#define FOR(i,l,r) for(int i=l;i<=r;i++)
#define FOD(i,r,l) for(int i=r;i>=l;i--)
#define ii pair<int,int>
#define iii pair<int,ii>
#define di pair<ii,ii>
#define vi vector<int>
#define vii vector<ii>
#define mii map<int,int>
#define fi first
#define se second
#define pb push_back
#define MOD 1000000007
#define __lcm(a,b) (1ll * ((a) / __gcd((a), (b))) * (b))
#define YES cout << "YES\n"
#define NO cout << "NO\n"
#define MASK(i) (1LL << (i))
#define c_bit(i) __builtin_popcountll(i)
#define BIT(x,i) ((x) & MASK(i))
#define SET_ON(x,i) ((x) | MASK(i))
#define SET_OFF(x,i) ((x) & ~MASK(i))
#define oo 1e18
#define name ""
#define endl '\n'
#define time() cerr << endl << "-------------Time:" << 1000.0 * clock() / CLOCKS_PER_SEC << "ms.";
template<typename T> bool maximize(T &res, const T &val) { if (res < val){ res = val; return true; }; return false; }
template<typename T> bool minimize(T &res, const T &val) { if (res > val){ res = val; return true; }; return false; }
const int N = (int)1e6+10;
int x[N],n,mod;
bool b[N];

void sang()
{
	fill(b,true);
	b[0] = b[1] = false;
	x[0] = x[1] = 0;
	FOR(i,2,sqrt(N-10))
		if (b[i])
			for (int j = sqr(i); j <= N-10; j += i)
			{
				if (!x[j]) x[j] = i;
				b[j] = false;
			}
	FOR(i,2,N-10)
		if (b[i]) x[i] = i;
}

namespace hungeazy {

	int mp[N];

	void solve(void)
	{
		FOR(i,1,n)
		{
			int val = i, s = 1, tmp = x[val];
			while (val != 1)
			{
				int cnt = 0;
				while (val%tmp == 0) val /= tmp, cnt++;
				if (cnt&1) s *= tmp;
				tmp = x[val];
			}
			mp[s]++;
		}
		int ans = 1;
		FOR(i,1,n) (ans *= (mp[i]+1)%mod) %= mod;
		cout << ans;
	}
	
}

signed main()
{
    fast;
    if (fopen(name".inp","r"))
    {
    	freopen(name".inp","r",stdin);
    	freopen(name".out","w",stdout);
    }
    sang();
    cin >> n >> mod;
    hungeazy::solve();
    time();
    return 0;
}
// ██░ ██  █    ██  ███▄    █   ▄████
//▓██░ ██▒ ██  ▓██▒ ██ ▀█   █  ██▒ ▀█▒
//▒██▀▀██░▓██  ▒██░▓██  ▀█ ██▒▒██░▄▄▄░
//░▓█ ░██ ▓▓█  ░██░▓██▒  ▐▌██▒░▓█  ██▓
//░▓█▒░██▓▒▒█████▓ ▒██░   ▓██░░▒▓███▀▒
// ▒ ░░▒░▒░▒▓▒ ▒ ▒ ░ ▒░   ▒ ▒  ░▒   ▒
// ▒ ░▒░ ░░░▒░ ░ ░ ░ ░░   ░ ▒░  ░   ░
// ░  ░░ ░ ░░░ ░ ░    ░   ░ ░ ░ ░   ░
// ░  ░  ░   ░              ░       ░

```
  
</td>
<td>

```cpp
// ~~ icebear ~~
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
typedef pair<int, int> ii;
typedef pair<ii, int> iii;

#define FOR(i,a,b) for(int i=(a); i<=(b); ++i)
#define FORR(i,a,b) for(int i=(a); i>=(b); --i)
#define rep(i, n) for(int i=0; i<(n); ++i)
#define red(i, n) for(int i=(n)-1; i>=0; --i)
#define mp make_pair
#define pb push_back
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define task "icebearat"

const int MOD = 1e9 + 7;
const int inf = 1e9 + 27092008;
const ll LLinf = 1e18 + 27092008;
const int N = 1e6 + 5;
int n, mod, f[N];
int dp[N];

void sieve() {
	FOR(i, 1, n) f[i] = i;
	FOR(i, 2, n)
		if (f[i] == i)
			for(int j = 2 * i; j <= n; j += i)
				f[j] = min(f[j], i);
}

void solve() {
	cin >> n >> mod;
	sieve();
	FOR(i, 1, n) {
		int x = i, left = 1;
		while(x > 1) {
			int t = f[x], cnt = 0;
			while(f[x] == t) {
				x /= t;
				cnt++;
			}
			if (cnt & 1) left *= t;
		}
		dp[left]++;
	}
	int ans = 1;
	FOR(i, 1, n) ans = 1LL * ans * (dp[i] + 1) % mod;
	cout << ans;
}

int main() {
	ios_base::sync_with_stdio(0);
	cin.tie(0); cout.tie(0);
	if (fopen(task".inp", "r")){
		freopen(task".inp", "r", stdin);
		freopen(task".out", "w", stdout);
	}
	int tc = 1;
//     cin >> tc;
	while(tc--) solve();
	return 0;
}

```

</td>
</tr>
</table>

# Code sau khi đã được tối giản bằng việc xóa đi các comment và template

Đây là phần code giống nhau

<table>
<tr>
    <th>hungeazy</th>
    <th>icebear_o</th>
</tr>
<tr>
<td>
  
```cpp
FOR(i,1,n){
    int val = i, s = 1, tmp = x[val];
    while (val != 1){
        int cnt = 0;
        while (val%tmp == 0)
            val /= tmp, cnt++;
        if (cnt&1) s *= tmp;
        tmp = x[val];
    }
    mp[s]++;
}
int ans = 1;
FOR(i,1,n)
    (ans *= (mp[i]+1)%mod) %= mod;
cout << ans;
```
  
</td>
<td>

```cpp
FOR(i, 1, n){
    int x = i, left = 1;
    while (x > 1){
        int t = f[x], cnt = 0;
        while (f[x] == t){
            x /= t;
            cnt++;
        }
        if (cnt & 1)
            left *= t;
    }
    dp[left]++;
}
int ans = 1;
FOR(i, 1, n)
    ans = 1LL * ans * (dp[i] + 1) % mod;
cout << ans;
```

</td>
</tr>
</table>
