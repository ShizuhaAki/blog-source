---
title: "Daily Practice: Oct 18, 2023"
date: 2023-10-18 15:55:51
tags: xcpc, dp, knapsack
---
Problem of the day: [CF1864D](https://codeforces.com/contest/1864/problem/D), *1800

## Analysis
As casting spells take no time, we can first fill up with mana and then deal with the monsters.

A naive thought would be to simply binary search for the answer, and then check whether the total mana acquired is enough to defeat all monsters. However, note that a monster could be killed with only one kind of magic (you can't use 5 points of water followed by 2 points of fire), this won't work.

However, we can be greedy. Let's say we try to use water magic as much as possible, then we resort to using fire magic. In this way, we can ensure that no monster shall lie on the borders. However, we can't just naively use the given ordering, as this might not be optimal (i.e. we might leave a huge pile of water mana). Instead, we use knapsacks. Compute the maximum number of monsters defeatable using water magic, and leave the rest to fire magic.

## Solution
```cpp
int a[N], dp[1001000];
void Main() {
    ll W, F;
    int n;
    rd(W, F);
    rd(n);
    ll S = 0;
    repn(i, n) {
        rd(a[i]);
        S += a[i];
    }
    rep(i, S + 1) dp[i] = 0;
    repn(i, n) {
        repd(j, S, 1) {
            if (j >= a[i]) {
                dp[j] = max(dp[j], dp[j - a[i]] + a[i]);
            }
        }
    }
    ll L = 0, R = 1e6, ans = -1;
    while (L <= R) {
        ll t = midpoint(L, R);
        if (F * t >= S - dp[min(S, W * t)]) {
            ans = t;
            R = t - 1;
        } else {
            L = t + 1;
        }
    }
    cout << ans << endl;
}
```