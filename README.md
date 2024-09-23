A.
Tưởng tưởng thang máy di chuyển theo chu kỳ rồi đến 1 và m từ đó suy công thức ra.
Code mẫu:
/*
    User: Nart
    Name: Elevator
    URL: https://codeforces.com/contest/117/problem/A
    Time Limit: 1s
    Memory Limit: 256 MB
*/
#include <bits/stdc++.h>
#define ll long long
#define int long long
using namespace std;
const int MAXN = 1e5 + 7;
int n, m;
int s[MAXN], f[MAXN], t[MAXN];

ll dis(int s, int t)
{
    return abs(s - t);
}

signed main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    #define Nart "Elevator"
    if(fopen(Nart".inp", "r"))
    {
        freopen(Nart".inp", "r", stdin);
        freopen(Nart".out", "w", stdout);
    }
    cin >> n >> m;
    ll time = 0;
    for (int i = 1 ; i <= n ; ++i)
    {
        cin >> s[i] >> f[i] >> t[i];
        if (s[i] == f[i])
        {
            cout << t[i] << '\n';
            continue;
        }
        time = t[i] / (2 * m - 2);
        time = time * (2 * m - 2);
        t[i] = t[i] % (2 * m - 2);

        if (s[i] < f[i])
        {
            if (t[i] >= m)
            {
                time += (2 * m - 2);
                t[i] = 0;
            }
//            cout << time << '\n';
            if (s[i] > t[i]) time += dis(1, f[i]);
            else time += (2 * m - 2) + (f[i] - 1);

        }
        else /// s[i] > f[i]
        {
            if (t[i] < m)
            {
                time += dis(1, m);
                t[i] = m;
            }
            else
            {
                time += dis(1, m);
                t[i] = m - (t[i] % (m - 1));
            }
//            cout << t[i] << '\n';

            if (s[i] <= t[i]) time += dis(m, f[i]);
            else time += (2 * m - 2) + dis(m, f[i]);
        }
        cout << time << '\n';
    }
    return 0;
}
B.
Vì nó thg a là a * 1000000000 nên chúng ta chỉ cần tìm giá trị a min sao cho (mod – a * 1e9) % mod > b:
/*
    User: Nart
    Name: B. Very Interesting Game
    URL: https://codeforces.com/contest/117/problem/B
    Time Limit: 2s
    Memory Limit: 256 MB
*/
#include <bits/stdc++.h>
#define ll long long
#define int long long
using namespace std;

int a, b, mod;
const int e9 = 1e9;
signed main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    #define Nart "B"
    if(fopen(Nart".inp", "r"))
    {
        freopen(Nart".inp", "r", stdin);
        freopen(Nart".out", "w", stdout);
    }
    cin >> a >> b >> mod;
    int ans = -1;
    for (int i = 0 ; i <= min(mod, a) ; ++i)
    {
        if (((mod - (i * e9 % mod)) % mod) > b)
        {
            cout << 1 << " ";
            ans = i;
            while (ans < 1e8)
            {
                cout << 0;
                ans *= 10;
            }
            cout << i;
            return 0;
        }
    }
    cout << 2;
    return 0;
}
C.
Dfs check nhu bthg:
/*
    User: Nart
    Name: C. Cycle
    URL: https://codeforces.com/contest/117/problem/C
    Time Limit: 2.5s
    Memory Limit: 256 MB
*/
#include <bits/stdc++.h>
#define ll long long
#define pii pair < int , int >
#define fi first
#define se second

using namespace std;

const int MAXN = 5005;
int n;
char a[MAXN][MAXN];
int used[MAXN], vi[MAXN];
int ok = 0, cnt = 0;

void dfs(int u)
{
    if (ok) return;
    used[u] = 1;
    vi[cnt++] = u;

    for (int v = 1 ; v <= n ; ++v)
    {
        if (a[u][v] == '1' && used[v] == 1)
        {
            ok = 1;
            cout << u << ' ' << v << ' ' << vi[cnt - 2] << '\n';
            exit(0);
        }
    }

    for (int v = 1 ; v <= n ; ++v)
    {
        if (a[u][v] == '1' && used[v] == 0)
        {
            dfs(v);
        }
    }
    cnt--;
    used[u] = 2;
    return;
}

signed main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    #define Nart "C"
    if(fopen(Nart".inp", "r"))
    {
        freopen(Nart".inp", "r", stdin);
        freopen(Nart".out", "w", stdout);
    }
    cin >> n;
    for (int i = 1 ; i <= n ; ++i)
    {
        for (int j = 1 ; j <= n ; ++j) cin >> a[i][j];
    }
    for (int i = 1 ; i <= n ; ++i)
    {
        if (!used[i])
            dfs(i);
    }
    if (!ok) cout << -1;
    return 0;
}
