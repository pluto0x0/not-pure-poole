---
title: 一些题目
math: true
tags:
- 构造
- 数学
categories: 杂

---

## CF 1600E

得到一个性质：只有从头开始的连续上升子串才能被取（因为要求每次取的数是严格递增的），结尾也是一样。

于是只需要考虑前 $$p$$ 个和后 $$q$$ 个数。

- 当 $$p$$ $$q$$ 都是偶数时，显然后手必胜（每次都取先手取的数的后一个数）
- 当 $$p$$ $$q$$ 有一个奇数时，显然先手必胜（第一步取奇数侧，变成必败态）
- 当 $$p$$ $$q$$ 都为奇数时，先手必胜（取第一项大的那一侧，该侧为必败，另一侧无法取）



```cpp
int main()
{
    // read input
    cin >> N;
    vi a(N);
    FOR(i, 0, N){
        cin >> a[i];
    }
    
    
    // find max left increasing sequence
    int p1 = 1;
    for(; p1 < N; p1++){
        if(a[p1-1] >= a[p1])
            break;
    }
 
    // find max right increasing sequece
    int p2 = 1;
    for(int pi = N - 2; pi >= 0; p2++, pi--){
        if(a[pi+1] >= a[pi])
            break;
    }
    
    // find who win
    cout << ((p1 % 2 || p2 % 2)  ? "Alice" : "Bob");
    // print result
 
}
```



# gym 100512

[Andrew Stankevich Contest 42](https://codeforces.com/gym/100512/attachments/download/2773/20122013-summer-petrozavodsk-camp-andrew-stankevich-contest-42-asc-42-en.pdf)

## D

换根lca

就是 $$1\leftrightarrow \texttt{root}$$ 的路径调个头

```cpp
int solve(int x,int y){	//get LCA of x, y
    int fx = lca(x,root), fy = lca(y,root);
    if(fx == fy) return lca(x,y);
    return dep[fx] > dep[fy] ? fx : fy;
}
```

## C

N/A

## B

暴力dp必然超时，考虑每次输的概率更大，最优策略就是每次押尽量多

# gym 100851

[ACM ICPC 2015–2016, Northeastern European Regional Contest](https://codeforces.com/gym/100851/attachments/download/3961/20152016-acmicpc-northeastern-european-regional-contest-neerc-15-en.pdf)

## B

求第 $k$ 大的“十进制表示为二进制表示的后缀”的数。

- 若 $$\overline{1A}$$ 合法，则 $$\overline{A}$$ 也合法，因为 $$10^n$$ 的二进制表示末尾必然也是 $$n$$ 个 $$0$$。

于是只要再所有 $$\le 2^n-1$$ 合法的数加上 $$2^n$$ ，留下合法的结果，就是所有$$\le 2^{n+1}$$ 合法的数。

```python
import math
inf = open('binary.in', 'r')
n = int(inf.readline())
a=[0,1]
b=[0,1]
for i in range(1,170):
    l=len(a)
    for j in range(0,l):
        if (a[j]+10**i-b[j]-2**i) % 2**(i+1)==0:
            a.append(a[j]+10**i)
            b.append(b[j]+2**i)
                     
with open("binary.out", 'w') as f:
    f.write(str(a[n]))
```

## L

二分最高点的高度。

[具体实现](https://codeforces.com/group/cTjYaoMsCo/contest/347707/submission/130946189)比较恶心。

## G

见 [完整题解](/upload/document.pdf)

# HDU某比赛

[2021中国大学生程序设计竞赛（CCPC）- 网络选拔赛（重赛）](https://acm.hdu.edu.cn/contest/problems?cid=1038)

## 1008

分类推式子。

具体见 [完整题解](/upload/2021中国大学生程序设计竞赛（CCPC）- 网络选拔赛（重赛）-题解.pdf)

## 1010

经过尝试，发现二分图需要连成一个环（显然每个点至少两条边，因此一定是最优解，并且一定能连成一个环）

字典序最小，大概就是维护并查集+贪心。

## 1011

想了很久。。

具体见 [完整题解](/upload/2021中国大学生程序设计竞赛（CCPC）- 网络选拔赛（重赛）-题解.pdf)

