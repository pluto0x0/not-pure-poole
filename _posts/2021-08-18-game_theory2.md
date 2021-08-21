---
title: 博弈例题练习
tags: [博弈论]
categories: 数学
toc:  true
math: true
---

## luogu P5765

### Problem

[题目](https://www.luogu.com.cn/problem/P5675)

 $$n$$ 堆石头，从中选择若干堆，进行Nim游戏，并规定先手取的第一堆。问先手必败的方案数量。

### Solution

枚举第一步取第 $$k$$ 堆，对于剩下的 $$n-1$$ 堆dp， $$f_{i}$$ 表示这 $$n-1$$ 堆中异或和为 $$i$$ 的方案数。

这部分的答案为 $$\sum\limits_{i \ge a_k}f_i$$ 

### Code

```cpp
#include <bits/stdc++.h>
#define rep(i, a, b) for (int i = (a); i <= (b); i++)
#define per(i, a, b) for (int i = (a); i >= (b); i--)
#define D(x) cout << #x << " : " << x << endl
using namespace std;
typedef long long ll;
const ll mod = 1e9 + 7;
const int N = 211;
ll f[2][256];

int n;
ll a[N];

int main() {
    cin.tie(0);
    ios::sync_with_stdio(false);

    cin >> n;
    rep(i, 1, n) cin >> a[i];

    ll ans = 0;
    bool op = 0;
    rep(i, 1, n) {
        memset(f[op], 0, sizeof f[op]);
        f[op][0] = 1;
        rep(j, 1, n) {
            if (j == i) continue;
            op = !op;
            memset(f[op], 0, sizeof f[op]);
            rep(k, 0, 255) {
                (f[op][k] += f[!op][k]) %= mod;
                (f[op][k ^ a[j]] += f[!op][k]) %= mod;
            }
        }
        rep(j, a[i], 255) (ans += f[op][j]) %= mod;
    }
    cout << ans << endl;
    return 0;
}
```

## luogu P2148

### Problem

[problem](https://www.luogu.com.cn/problem/P2148)

### Solution

一个状态（两堆石头）用 $$(x,y)$$ 表示

 $$sg(x,y) = f((x-1)\vert (y-1))$$ 

其中 $$\vert$$ 表示按位或运算， $$f(x)$$ 表示 $$x$$ 的二进制表示下 $$0$$ 出现的最小位置（从位置0开始）。

证明：打表。。。[题解](https://www.luogu.com.cn/blog/Sooke/solution-p2148)

### Code

```cpp
#include <bits/stdc++.h>
#define rep(i, a, b) for (int i = (a); i <= (b); i++)
#define per(i, a, b) for (int i = (a); i >= (b); i--)
#define D(x) cout << #x << " : " << x << endl
using namespace std;
const int N = 20011;

int T;
int n, a[N];

int f(int x) {
    int ans = 0;
    while (x % 2) {
        ans++;
        x /= 2;
    }
    return ans;
}

int main() {
    cin.tie(0);
    ios::sync_with_stdio(false);

    cin >> T;
    while (T--) {
        int ans = 0;
        cin >> n;
        rep(i, 1, n / 2) {
            int x, y;
            cin >> x >> y;
            ans ^= f((x - 1) | (y - 1));
        }
        cout << (ans ? "YES" : "NO") << endl;
    }
    return 0;
}
```


