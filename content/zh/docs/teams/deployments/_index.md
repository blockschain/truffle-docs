---
title: 部署概述
linkTitle: 部署
weight: 7
---

Truffle Teams 提供了一种快速简便的界面，用于将智能合同部署到 Ethereum Testnets，Mainnet 和[Sandboxes](/docs/teams/sandboxes/sandboxes-overview).
在 **<span class="inline-menu-item"><i class="fal fa-parachute-box"></i>DEPLOYMENTS</span>** 页上, 您可以在两个视图之间切换: [cards](#cards-view) 和 [table](#table-view).

## 卡片视图

**CARDS** 视图包含三列: **Commits**, **Staging**, and **Production**.
这些列包含可用于部署的构建以及任何成功的部署。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/deployments-card-view.png" alt="Deployments cards view" style="width: 100%">
  <figcaption class="text-center font-italic">部署卡视图</figcaption>
</figure>

### 构建专栏

**Builds** 是松露团队正在处理或已处理的所有构建的列表。
每个都将有一个状态图标来显示构建是否正在进行，失败或成功。
使用成功的图标建立（具有复选标记的绿色框，如图所示）将能够部署; 提交右上角的 **<span class="inline-button">DEPLOY <i class="far fa-parachute-box"></i></span>** 按钮表示此.

<figure>
  <img class="mb-2" src="/img/docs/teams/commit-card.png" alt="Commit Card">
</figure>

### 分期和生产柱

**Staging** 包含所有 TestNet 的列表（即 Ropsten，Görli，rinkeby 和 kovan）以及沙箱部署。
**Production** 包含 MainNet 部署的列表。

## 表视图

**TABLE** 视图包含所有成功部署的列表，无论它们部署到哪个网络。
有一个**NETWORK** 列，表示部署部署的网络。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/deployments-table-view.png" alt="部署表视图" style="width: 100%">
  <figcaption class="text-center font-italic">部署表视图</figcaption>
</figure>
