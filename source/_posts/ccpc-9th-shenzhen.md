---
title: 第九届 CCPC 深圳站参赛报告
date: 2023-11-14 19:48:07
tags: [xcpc, zh, report]
---

## 热身赛
热身赛的题目是 THUPC 的往年赛题，我们前一个小时认真做了 AB 两题，后一个小时进行了系统测试，包括

- CE 算不算罚时？（不算）
- WA1 算不算罚时？（算）
- 提交时需要选择语言，且不选择将默认为 C

## 正赛
9：00 进场后开题。按照往届 VP 的经验，一般在 3 分钟左右就会有人过题，但这次比赛直到 10 分钟左右才出现过题。由于平常我们队伍几乎永远处于有榜可跟的状态，我们并没有练出判断题目可做性的能力。这使得比赛开始浪费了不少时间。

9：20 左右基本可以看出 AL 两题是签到题。因此开始做 A，ttb 提出了一个分块做法，我粗略估算是 $O(n\sqrt{n})$ 量级，但他证明了上限只是略微超过 20000，并且“很松”，因此能过。于是喂给我做法。我上机写 A。A 的这个分块做法写起来很复杂，有不少边界条件需要判断，因此写的很急。9：40 发现 F 也是可做题，xzk 迅速推出了基环树上的计数方法，于是他上机开写，稍微调试一段时间后便通过。

之后我继续上机写 A，xzk 和 ttb 讨论 L 的做法，他们很快推出了正解 DP 式子。我的 A 通过了样例，但极限数据测试需要的操作数超过了题目要求。于是我让机给 L。L 很快通过了样例，但是提交后超时，后来发现极限数据在 O2 后要跑到 4s。

这时已经快到了 2h，我仍然没有想到如何压缩 A 的操作次数，这时 ttb 想到了 A 的正确构造——二分，这是 $O(n \log n)$ 级的，明显可以通过。但此时我奋战了两小时的做法被完全无效化，对我的心态产生了不小的影响。我也犯了向队友输出情绪的大错。

xzk（代码核心！）上机写出了 A，调试的时候崩掉了我的 checker，一开始以为 checker 写的有问题，于是又吃了一发罚时，后来发现 checker 在非法输出的时候会崩溃，改掉后过了 A

此时时间为 2 小时 40 分钟，我带着 A 的错误做法想 G 并几乎立刻想到了哈希+分块的正解，喂给 xzk 后吃了两发罚时，最后改了一个似乎不会影响正确性的小点后通过。

时间来到 3 小时。我们全队开始卡 L 的常无果，同时 ttb 去做 I 题，xzk 提了一嘴数据分治之后去写了 $k \ge 4$ 的情况，同时 ttb 开始数学推导，最终推出了 $k=3$ 的正解 Observation。需要一些 STL，因此我上机写了 $k=3$ 的情况，一段调试后过样例并吃 WA。此时到了 4h。

最后一个小时我们一起试图调出 L 和 I，由于 L 通过人数很多，我们对自己的做法产生了很大的怀疑，几度决定换做法但也想不出有效的做法。而 I 则不断发现小错误，在代码上打了很多补丁最后也没有通过。最终因为高罚时而遗憾铁牌离场。

## 总结和自我批判
### SS
本场比赛我犯了很多错误，其中最重要的一点便是情绪管理。我在自己负责的分块程序不正确之后便有些情绪失控，这样的失控几乎贯穿了全场比赛。同时，我个人的代码能力偏向于模拟/STL等，思维能力较弱，这就导致在写很多题目的时候都难以独自输出，必须依赖队友。这是以后个人训练时必须加强的。

### TTB
虽然正赛连键盘都没碰，但是我还是觉得这场发挥没太大问题，在误差允许范围内。A的分块假做法确实大锅，不过好在最后还是喂了真做法，xzk五分钟直接拿下。I题其实也应该有能力把$k=3$的二分做法推广到$k\ge 4$从而改善最后的程序的，可惜当时一直执着于WA了什么数据，没想过这种优化方法。
之后感觉保持这样状态也行，不过既然不怎么写代码就更要多做题，熟悉一下建模套路，免得I这种其实很简单的题却开太晚而且最后都没过。

### XZK
自我批判：平时我写代码都不太注重罚时，这次到后面也有些心急甚至直接开莽，这导致了代码中出现了很多小漏洞，吃了很多罚时，在以后的模拟和比赛中要多加注意。一些代码常见错误要在写时就避免（多测清空，注意空间大小，注意数组下标）。平时看见一些常用技巧要多注意。板子的多样性。
