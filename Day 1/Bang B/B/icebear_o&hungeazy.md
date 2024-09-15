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
* @Date:   2024-09-14 18:35:11
* @Last Modified by:   hungeazy
* @Last Modified time: 2024-09-14 19:38:28
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
const int N = (int)1e6+10, base = 31;
vector<vector<char>> a;
int n,m,q;

namespace sub12 {

	int p[N];
	vector<vi> hashA,hashB;

	int hashing(int hashVal, char h)
	{
		return (hashVal*base+h-'a'+1)%MOD;
	}

	int getHashA(int l, int r, int i)
	{
		return (hashA[i][r]-hashA[i][l-1]*p[r-l+1]%MOD+sqr(MOD))%MOD;
	}

	int getHashB(int l, int r, int i)
	{
		return (hashB[r][i]-hashB[l-1][i]*p[r-l+1]%MOD+sqr(MOD))%MOD;
	}

	void solve(void)
	{
		hashA.resize(n+1,vi(m+1,0));
		hashB.resize(n+1,vi(m+1,0));
		p[0] = 1;
		FOR(i,1,n*m) p[i] = p[i-1]*base%MOD;
		FOR(i,1,n)
		{
			string st = "";
			FOR(j,1,m) st = st+a[i][j];
			// cout << st << endl;
			int len = st.size();
			st = '#'+st;
			FOR(j,1,len) hashA[i][j] = hashing(hashA[i][j-1],st[j]);
		}
		FOR(i,1,m)
		{
			string st = "";
			FOR(j,1,n) st = st+a[j][i];
			// cout << st << endl;
			int len = st.size();
			st = '#'+st;
			FOR(j,1,len) hashB[j][i] = hashing(hashB[j-1][i],st[j]);
		}
		while (q--)
		{
			string s;
			cin >> s;
			int hashC = 0, len = s.size();
			s = '#'+s;
			FOR(i,1,len) hashC = hashing(hashC,s[i]); 
			FOR(i,1,n)
				FOR(j,1,m-len+1)
					if (getHashA(j,j+len-1,i) == hashC) 
					{
						cout << 1;
						goto li;
					}
			FOR(i,1,m)
				FOR(j,1,n-len+1)
					if (getHashB(j,j+len-1,i) == hashC)
					{
						cout << 1;
						goto li;
					}
			cout << 0;
			li:;
		}
	}
	
}

namespace sub3 {

	vii pos[27];
	
	void solve(void)
	{
		FOR(i,1,n)
			FOR(j,1,m) pos[a[i][j]-'a'+1].pb({i,j});
		while (q--)
		{
			string s;
			cin >> s;
			int len = s.size();
			s = '#'+s;
			for (ii val : pos[s[1]-'a'+1])
			{
				int x = val.fi, y = val.se, cnt1 = 0, cnt2 = 0;
				FOR(i,1,len)
				{
					if (x+i-1 <= n and a[x+i-1][y] == s[i]) cnt1++;
					if (y+i-1 <= m and a[x][y+i-1] == s[i]) cnt2++;
				}
				if (cnt1 == len or cnt2 == len) 
				{
					cout << 1;
					goto li;
				}
			}	
			cout << 0;
			li:;
		}
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
    cin >> n >> m >> q;
    a.resize(n+1,vector<char>(m+1));
    FOR(i,1,n)
    	FOR(j,1,m) cin >> a[i][j];
    // if (n*m <= 1e4) sub12::solve();
    // else 
    sub3::solve();
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
#include <bits/stdc++.h>
using namespace std;

#define int long long
#define FOR(i, a, b) for(int i = (a); i <= (b); i++)
#define FORR(i, a, b) for(int i = (a); i >= (b); i--)
#define all(x) x.begin(), x.end()
#define task " "

const int MOD = 1e9 + 7;
const int base = 311;
const int N = 2e5 + 5;
int n, m, q;
vector<vector<char>> a;
vector<pair<int, int>> pos[26];

signed main() {
	ios_base::sync_with_stdio(0); 
	cin.tie(0); cout.tie(0);
	if (fopen(task".inp", "r")) {
		freopen(task".inp", "r", stdin);
		freopen(task".out", "w", stdout);
	}
	
	cin >> n >> m >> q;
	a.resize(n + 5, vector<char>(m + 5));

	FOR(i, 1, n)
		FOR(j, 1, m) cin >> a[i][j];

	FOR(i, 1, n) {
		FOR(j, 1, m) {
			pos[a[i][j] - 'a'].emplace_back(i, j);
		}
	}

	while(q--) {
		string s;
		cin >> s;
		bool ok = false;
		for(auto e : pos[s[0] - 'a']) {
			int x, y; tie(x, y) = e;
			int cnt1 = 0, cnt2 = 0;
			FOR(i, 0, (int)s.size() - 1) {
				if (x + i <= n && a[x + i][y] == s[i])
					cnt1++;
				if (y + i <= m && a[x][y + i] == s[i])
					cnt2++;
			}
			if ((cnt1 == (int)s.size() || cnt2 == (int)s.size()))
				ok = true;
		}

		cout << ok;
	}

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
while (q--){
	string s;
	cin >> s;
	int len = s.size();
	s = '#'+s;
	for (ii val : pos[s[1]-'a'+1]){
		int x = val.fi, y = val.se, cnt1 = 0, cnt2 = 0;
		FOR(i,1,len){
			if (x+i-1 <= n and a[x+i-1][y] == s[i])
				cnt1++;
			if (y+i-1 <= m and a[x][y+i-1] == s[i])
				cnt2++;
		}
		if (cnt1 == len or cnt2 == len) {
			cout << 1;
			goto li;
		}
	}	
	cout << 0;
	li:;
}
```
</td>
<td>

```cpp
while(q--) {
	string s;
	cin >> s;
	bool ok = false;
	for(auto e : pos[s[0] - 'a']) {
		int x, y; tie(x, y) = e;
		int cnt1 = 0, cnt2 = 0;
		FOR(i, 0, (int)s.size() - 1) {
			if (x + i <= n && a[x + i][y] == s[i])
				cnt1++;
			if (y + i <= m && a[x][y + i] == s[i])
				cnt2++;
		}
		if ((cnt1 == (int)s.size() || cnt2 == (int)s.size()))
			ok = true;
	}

	cout << ok;
}
```

</td>
</tr>
</table>