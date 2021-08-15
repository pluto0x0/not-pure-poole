---
math: true
title: C++lambda表达式的简单应用

---

<https://www.cnblogs.com/DswCnblog/p/5629165.html>

```cpp
// 规定返回值类型
sort(a + 1, a + 1 + n, [](int x, int y) -> bool { return x > y; });
// 自动推断返回值类型
sort(a + 1, a + 1 + n, [](int x, int y) { return x > y; });
```
