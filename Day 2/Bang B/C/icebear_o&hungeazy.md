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
* @Date:   2024-01-24 17:33:29
* @Last Modified by:   hungeazy
* @Last Modified time: 2024-09-15 20:15:31
*/
#include <bits/stdc++.h>
#pragma GCC optimize("O3")  
#pragma GCC optimize("unroll-loops")  
#pragma GCC target("avx2,bmi,bmi2,popcnt,lzcnt")  
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
#define time() cout << "-------------Time:" << 1000.0 * clock() / CLOCKS_PER_SEC << "ms.";
template<typename T> bool maximize(T &res, const T &val) { if (res < val){ res = val; return true; }; return false; }
template<typename T> bool minimize(T &res, const T &val) { if (res > val){ res = val; return true; }; return false; }
const int N = (int)1e6+10;
int dp[N],cnt[N],down[N],up[N],n,f[N];
vi g[N];
 
void DFS(int u, int p)
{
	cnt[u] = 1;
	for (int v : g[u])
		if (v != p)
		{
			DFS(v,u);
			cnt[u] += cnt[v];
			down[u] += down[v]+cnt[v];
			f[u] += cnt[v]+2*down[v]+f[v];
		}
}
 
void DFS2(int u, int p)
{
	dp[u] = f[u];
	for (int v : g[u])
		if (v != p)
		{
			ii x = {f[u],f[v]}, y = {cnt[u],cnt[v]}, z = {down[u],down[v]};
			f[u] -= cnt[v]+2*down[v]+f[v];
			down[u] -= down[v]+cnt[v];
			cnt[u] -= cnt[v];
			cnt[v] += cnt[u];
			down[v] += down[u]+cnt[u];
			f[v] += cnt[u]+2*down[u]+f[u];
			DFS2(v,u);
			f[u] = x.fi; f[v] = x.se;
			cnt[u] = y.fi; cnt[v] = y.se;
			down[u] = z.fi; down[v] = z.se;
		}
}
 
signed main()
{
    fast;
    // freopen(name".inp","r",stdin);
    // freopen(name".out","w",stdout);
    cin >> n;
    FOR(i,1,n-1)
    {
    	int u,v;
    	cin >> u >> v;
    	g[u].pb(v); g[v].pb(u);
    }
    DFS(1,-1); DFS2(1,-1);
    FOR(i,1,n) cout << dp[i] << endl;
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
#define int long long
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
const int N = 2e5 + 5;
int n;
vector<int> G[N];
int sz[N], dist[N], f[N];
int ans[N];

void DFS(int u, int par) {
	sz[u] = 1;
	for(int v : G[u]) {
		if (v == par) continue;
		DFS(v, u);
		int w = 1;
		sz[u] += sz[v];
		dist[u] += dist[v] + sz[v] * w;
		f[u] += sz[v] * w * w + 2 * dist[v] * w + f[v];
	}
}

void reroot(int u, int par) {
	ans[u] = f[u];
	for(int v : G[u]) {
		if (v == par) continue;
		ii F = mp(f[u], f[v]); 
		ii S = mp(sz[u], sz[v]);
		ii D = mp(dist[u], dist[v]);
		int w = 1;

		f[u] -= sz[v] * w * w + 2 * dist[v] * w + f[v];
		dist[u] -= dist[v] + sz[v] * w;
		sz[u] -= sz[v];

		sz[v] += sz[u];
		dist[v] += dist[u] + sz[u] * w;
		f[v] += sz[u] * w * w + 2 * dist[u] * w + f[u];

		reroot(v, u);

		tie(f[u], f[v]) = F;
		tie(sz[u], sz[v]) = S;
		tie(dist[u], dist[v]) = D;
	}
}

void solve() {
	cin >> n;
	FOR(i, 2, n) {
		int u, v;
		cin >> u >> v;
		G[u].pb(v);
		G[v].pb(u);
	}

	DFS(1, -1);
	reroot(1, -1);
	FOR(i, 1, n) cout << ans[i] << '\n';
}

signed main() {
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
void DFS(int u, int p){
	cnt[u] = 1;
	for (int v : g[u])
		if (v != p){
			DFS(v,u);
			cnt[u] += cnt[v];
			down[u] += down[v]+cnt[v];
			f[u] += cnt[v]+2*down[v]+f[v];
		}
}
 
void DFS2(int u, int p){
	dp[u] = f[u];
	for (int v : g[u])
		if (v != p){
			ii x = {f[u],f[v]}, y = {cnt[u],cnt[v]}, z = {down[u],down[v]};
			f[u] -= cnt[v]+2*down[v]+f[v];
			down[u] -= down[v]+cnt[v];
			cnt[u] -= cnt[v];
			cnt[v] += cnt[u];
			down[v] += down[u]+cnt[u];
			f[v] += cnt[u]+2*down[u]+f[u];
			DFS2(v,u);
			f[u] = x.fi; f[v] = x.se;
			cnt[u] = y.fi; cnt[v] = y.se;
			down[u] = z.fi; down[v] = z.se;
		}
}
```
  
</td>
<td>

```cpp
void DFS(int u, int par) {
	sz[u] = 1;
	for(int v : G[u]) {
		if (v == par) continue;
		DFS(v, u);
		int w = 1;
		sz[u] += sz[v];
		dist[u] += dist[v] + sz[v] * w;
		f[u] += sz[v] * w * w + 2 * dist[v] * w + f[v];
	}
}

void reroot(int u, int par) {
	ans[u] = f[u];
	for(int v : G[u]) {
		if (v == par) continue;
		ii F = mp(f[u], f[v]); 
		ii S = mp(sz[u], sz[v]);
		ii D = mp(dist[u], dist[v]);
		int w = 1;

		f[u] -= sz[v] * w * w + 2 * dist[v] * w + f[v];
		dist[u] -= dist[v] + sz[v] * w;
		sz[u] -= sz[v];

		sz[v] += sz[u];
		dist[v] += dist[u] + sz[u] * w;
		f[v] += sz[u] * w * w + 2 * dist[u] * w + f[u];

		reroot(v, u);

		tie(f[u], f[v]) = F;
		tie(sz[u], sz[v]) = S;
		tie(dist[u], dist[v]) = D;
	}
}

```

</td>
</tr>
</table>