---
layout: post
title: "USTC Lean 讨论班入门指南"
subtitle: 从零开始把数学定理敲给计算机看
tags: [Lean, 形式化, 讨论班]
---

每周固定时间，我们会在 USTC 数学楼里围坐一桌，盯着投影上一行行红蓝相间的语法 —— 这就是 Lean 形式化讨论班的日常。本文写给想加入但还不知从哪里下手的同学，也作为我自己的备忘录。

## 为什么搞形式化？

数学证明在纸上写出来时，「显然」、「类似可证」、「留作习题」出现的频率高得惊人。一旦把这些环节都填满，证明会膨胀几十倍。**形式化证明**就是把每一步都写到机器能够独立验证的颗粒度，由编译器替你检查是不是真的「显然」。

近几年这件事变得很热：

- 2020 年 Kevin Buzzard 团队在 Lean 里形式化了 perfectoid space；
- 2023 年 Terence Tao、Tim Gowers 等人用 Lean 验证了 PFR 猜想的证明；
- 到 2025 年，社区库 Mathlib 已经覆盖了本科数学绝大部分内容。

形式化不再是远方的科幻，而是一种实际可用的工具：写论文时核对自己的推理是否真的滴水不漏；做研究时把可疑的引理交给电脑试试看；当老师时把习题答案的对错完全脱手。

## 什么是 Lean

Lean 是一门以**依赖类型论**（dependent type theory）为基础的证明助手，由 Leonardo de Moura 在微软研究院主导开发。它的核心想法可以用 Curry–Howard 对应一句话概括：

> 命题就是类型，证明就是这个类型的元素。

也就是说，$a + b = b + a$ 不是一个待证明的句子，而是一个**类型**；要「证明它」就是要在这个类型里构造出一个具体的元素。Lean 的编译器负责检查你的构造是否真的属于这个类型 —— 通过了就是证明，没通过就是证错了。

一个最简单的例子：

```lean
example (a b : ℕ) : a + b = b + a := by
  ring
```

这段代码的意思是：「给我任意自然数 $a, b$，我能给出 $a + b = b + a$ 的证明」，然后用 `ring` 这个 tactic（自动验证交换环恒等式）一脚踢给机器。

## 讨论班在做什么

讨论班由数学学院研究生**孙天阳**学长牵头组织，我担任助教。每周一次，节奏大致是：

1. **主讲同学**讲约 1 小时，覆盖 Mathlib 的一个主题或一道定理的形式化；
2. **自由练习**约 1 小时，所有人对着同一份 `.lean` 文件填空，遇到困难当场提问；
3. **答疑总结**半小时，把当周大家踩到的坑写进 wiki。

讨论班的讲义、Beamer 源码、视频回放都放在 [github.com/cccyyylll888/Lean4-group](https://github.com/cccyyylll888/Lean4-group)。

## 怎么入门

如果你完全没碰过 Lean，**推荐这条路径**：

1. **装环境**。用 [elan](https://github.com/leanprover/elan) 装好 Lean 工具链，编辑器用 VS Code 加 `lean4` 插件。Windows 用户直接装 elan 的 Windows 版本即可，**不需要 WSL**。
2. **过 NNG**。[Natural Number Game](https://adam.math.hhu.de/) 是网页版的入门关卡，从 `rfl` 到 `induction` 两三个小时就能打通，无需本地安装。
3. **读 MIL**。[Mathematics in Lean](https://leanprover-community.github.io/mathematics_in_lean/) 是社区维护的教材，按章节对应 Mathlib 的主要分支，强烈建议跟着练。
4. **来讨论班**。每周固定时间和大家一起卡关，比一个人对着 Lean 的报错信息发呆愉快得多。

## 一个小练习

下面是 NNG 早期的一个练习，先在自己机器上把它跑通：

```lean
example (a b c : ℕ) : a + (b + c) = (a + b) + c := by
  rw [Nat.add_assoc]
```

`rw` 是 rewrite 的缩写，它把 `a + (b + c)` 按照 `Nat.add_assoc` 改写成 `(a + b) + c`，等号两边一致，Lean 自动收尾。如果你在自己机器上看到 `No goals` 的绿色提示，恭喜 —— 你已经写完了你的第一个 Lean 证明。

---

下一篇打算写：**怎么在 Mathlib 里搜到你想要的定理 —— Loogle、moogle、`exact?` 三件套**。

如果你也想加入讨论班，发邮件到 [cyl2500@mail.ustc.edu.cn](mailto:cyl2500@mail.ustc.edu.cn) 即可。
