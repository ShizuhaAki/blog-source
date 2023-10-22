---
title: "Daily Practice: Oct 22, 2023"
date: 2023-10-18 15:55:51
tags: [xcpc, dp, knapsack]
---
Problem of the day: [CF1856E1](https://codeforces.com/contest/1856/problem/E1)

## Analysis
It is easy to observe that we need to split the sizes of the subtrees evenly. The problem is transformed to the following basic pattern:

> Given an array $a$, find a way to partition $a$ into two parts, such that the difference between the sum of these two parts is minimized.

This can be solved via knapsack DP. Note that we don't need to calculate the sizes of subtrees before running the DP, we can do this while traversing the tree. The resulting time complexity is $O(n^2)$.

## Solution
```cpp
void dfs(int u, int f) {
    sz[u] = 1;
    bool hasChild = false;
    for (auto v : g[u]) {
        if (v == f) continue;
        hasChild = true;
        dfs(v, u);
        sz[u] += sz[v];
        ans[u] += ans[v];
    }
    if (hasChild) {
        memset(dp, 0, sizeof(dp));
        dp[0] = 1;
        for (auto v : g[u]) {
            if (v == f) continue;
            for (int i = sz[u]; i >= sz[v]; i--) chmax(dp[i], dp[i - sz[v]]);
        }
        int dans = 0;
        for (int i = sz[u] / 2; i >= 1; i--) {
            if (dp[i]) {
                chmax(dans, i * (sz[u] - i - 1));
            }
        }
        ans[u] += dans;
    }
}
void Main() {
    rd(n);
    repn(i, n - 1) {
        int f;
        rd(f);
        g[f].push_back(i + 1);
        g[i + 1].push_back(f);
    }
    dfs(1, 0);
    cout << ans[1] << endl;
}
```