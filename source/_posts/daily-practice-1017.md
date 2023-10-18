---
title: "Daily Practice: Oct 17, 2023"
date: 2023-10-17 23:11:45
tags: [xcpc, dp, constructive-algorithms]
---

Problem of the day: [CF1864D](https://codeforces.com/contest/1864/problem/D), *1700
## Analysis
The idea is pretty simple and cliche. Similar to the classical problem of flipping light bulbs on and off, with a light triggering every light bulbs surrounding it, all the operations we perform here can only affect numbers "below" the current number. Thus, we can fully determine what to do for the first row, and then the second row, until we get all the way to the bottom.

However, the real essence of this problem lies in: How do you actually keep account on this? You can't just do updates by brute-force, that'll be $O(n^4)$, we have to think of a better way.

Note that we don't actually need to traverse every cell. We only need the cell to know how should it be updated, and we can know about this by just asking the cells above it.

Thus, we keep track of three tags, `l`, `m`, and `r`. **Note that it'll be ugly if we don't keep tabs on `m`**. When we try to do an update, we push the tags down, just like in a segment tree. `l` gets pushed to the bottom-left, `m` the bottom, and `r` the bottom-right. 

We can solve this problem in $O(n^2)$.

## Solution
```cpp
void Main() {
    rd(n);
    repn(i, n) scanf("%s", a[i] + 1);
    repn(i, n) repn(j, n) a[i][j] -= '0';
    repn(i, n) repn(j, n) l[i][j] = m[i][j] = r[i][j] = 0;
    int ans = 0;
    repn(i, n) {
        repn(j, n) {
            if (m[i][j]) {
                a[i][j] ^= 1;
                l[i + 1][j - 1] ^= 1;
                m[i + 1][j] ^= 1;
                r[i + 1][j + 1] ^= 1;
            }
            if (l[i][j]) {
                a[i][j] ^= 1;
                l[i + 1][j - 1] ^= 1;
            }
            if (r[i][j]) {
                a[i][j] ^= 1;
                r[i + 1][j + 1] ^= 1;
            }
            if (a[i][j]) {
                ans++;
                l[i + 1][j - 1] ^= 1;
                m[i + 1][j] ^= 1;
                r[i + 1][j + 1] ^= 1;
            }
        }
    }
    cout << ans << endl;
}
```