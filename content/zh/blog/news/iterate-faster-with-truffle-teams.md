---
title: 用 Truffle 团队速度更快
date: 2021-02-10
author: "Josh Quintal"
published: true
description: 考虑开发DAPP所需的上下文切换量：您正在编写稳定性，一分钟，写入测试另一个，调试这些结果 - 很容易丢失！我很高兴地通知你Truffle团队可以帮助减少上下文切换并帮助您或您的团队迭代更快。
image: "/img/blog/iterate-faster-with-truffle-teams/blog-thumbnail.png"
---

考虑开发 DAPP 所需的上下文切换量: 你写了一分钟的稳定性，写作另一个测试，调试这些结果--很容易迷路!
这些交换机携带认知负载，并且当错误等于 ETH 的损失时，我们需要我们所能得到的所有帮助.
我很高兴地通知你， Truffle 团队可以帮助减少上下文切换，帮助您或您的团队迭代更快.

Truffle Teams 在其生命中达到了一个非常重要的阶段：它现在提供了一个完整的工作流程，包括构建，测试，管理，监控和调试.
这意味着你的生产力越来越大。
这适用于您和/或您的团队更强大的工作流程，并通过在灵活开发网络中收紧所有部署，操作和调试之间的反馈循环来贡献应用程序生命周期。

<figure>
  <img class="mb-4 w-100" src="/img/blog/iterate-faster-with-truffle-teams/dev-lifecycle.png" alt="The development lifecycle: plan, code, build, test, release, deploy, operate, and monitor.">
  <figcaption class="text-center font-italic">发展生命周期。</figcaption>
</figure>

截至目前，Truffle 团队已经提供构建系统，部署管理器，区块链沙箱和监控。
最近我们将视觉调试器发布到早期访问权限。
使用这一点，我们希望突出显示完成此循环的两个功能：调试器和合约管理器。

对于一个很好的视频示例，请从 Trufflecon 2020 查看我们的演示。我们简要触及使用岩石，纸张，剪刀游戏对上面谈到的所有阶段。
对于更长期的东西，请查看我们的 5 件网络研讨会系列，通过使用 Truffle Suite 来创建 NFT 并在分散的市场上进行交易。

<figure>
  <a href="https://www.youtube.com/watch?v=LsQ2Iwd5VMc" target="_blank">
    <img class="mb-4 w-100 w-md-70 figure-shadow" src="/img/blog/iterate-faster-with-truffle-teams/teams-demo-tcon-2020.jpg" alt="Josh Quintal和Mike的视频缩略图在Trufflecon 2020上看到了 Truffle 团队的演示。">
    <figcaption class="text-center font-italic">Mike Seese和Josh Quintal使用Troffle团队进行分散的岩石，纸，剪刀DAPP的整个开发生命周期。</figcaption>
  </a>
</figure>

## 调试器增强

<i class="fas fa-info-circle"></i> 注意: 要立即使用调试器，您需要选择选择 [ Truffle 队早期访问](/blog/try-new-features-first-with-truffle-teams-early-access).

Truffle 提供了一个复杂的法医事务调试器，并允许您从您的交易中提取可能的最多信息和上下文。
我们将指令行调试器的图形版发布到 12 月的 Truffle Teams 早期访问。从那以后，我们已经添加了改进的开发人员体验的语法突出显示和断点。
可读性增加，您可以控制执行停止，提供精确调试体验。
查看 Truffle Teams 调试器文档以了解有关断点的更多信息。
目前，Truffle 团队中的调试器只适用于沙盒环境，但我们计划接下来支持公共网络！

<figure class="breakout">
  <img class="mb-4 w-100 w-md-70 figure-shadow" src="/img/blog/iterate-faster-with-truffle-teams/debugger.png" alt="The Truffle Teams debugger working on an NFT-based badge contract">
  <figcaption class="text-center font-italic">The Truffle Teams调试器 - 现在有语法突出显示和断点！</figcaption>
</figure>

## 合约经理

<i class="fas fa-info-circle"></i> 注意: 要立即使用合约经理，您需要选择选择 [ Truffle 队早期访问](/blog/try-new-features-first-with-truffle-teams-early-access).

Truffle Teams 的合约管理器会生成一个用于与智能合约的所有功能进行交互的 UI，以及实时状态树，因此您可以快速查看这些功能传播的更改。
如果你熟悉混音，你会在这里感受到宾至如归。

<figure class="breakout">
  <img class="mb-4 w-100 w-md-70 figure-shadow" src="/img/blog/iterate-faster-with-truffle-teams/contract-manager.png" alt="Truffle团队使用基于NFT的徽章合约合约经理">
  <figcaption class="text-center font-italic">合约经理;在这里使用NFT徽章。</figcaption>
</figure>

合约经理非常适合快速演示，集成测试以及更快的 All-GUI 调试工作流程。
例如，您可以通过部署向导部署到沙盒，跳至合约管理器以解雇一些事务，最后从监控屏幕调试这些事务。

## dapp 形貌

前进，我们将帮助您了解您的 DAPP 甚至更深入的水平，提供对您交易的法医级别分析。
不仅如此，而且它将能够将合约互动绘制，以允许不同的利益相关者参与调试过程。
例如，产品管理器或其他域专家可以参与法医分析。
这些图表和其他资产可以是可以适合现有通信通道的可共享媒体。

<figure class="breakout">
  <img class="mb-4 w-100 w-md-70" src="/img/blog/iterate-faster-with-truffle-teams/ens-plant-uml.png" alt="ENS交易的植物UML图">
  <figcaption class="text-center font-italic">
  一个测试，其中不是ENS名称的所有者尝试更改解析程序的用户。
  注意显示恢复的“x”。</figcaption>
</figure>

## 开始用 Truffle 团队

我们希望 Truffle 团队成为新和现有团队的区块链空间中最有效的 Devops 工具。
立即查看 Truffle 团队，让我们知道您对新部署视图和合约经理的看法，或者您的团队还有其他需要我们还没有遇到过。

<div class="mt-3 mb-4 text-center">
  <a class="btn btn-truffle" href="https://my.truffleteams.com">注册 Truffle 团队</a>
  <a class="btn btn-truffle" href="/docs/teams/quickstart"> Truffle 队Quickstart.</a>
</div>

谢谢！

_JOSH Quintal，产品和营销负责人_
