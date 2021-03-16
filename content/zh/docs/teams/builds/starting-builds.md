---
title: 开始构建
weight: 2
---

一旦将新提交被推送到垃圾团队添加到块鼠队的任何存储库的任何分支，构建将自动启动。
Build 将排队在 Truffle 团队和 GitHub 上与承诺本身排队。

<figure>
  <img class="mb-2" src="/img/docs/teams/starting-builds-04.png" alt="GitHub build status">
</figure>

在进步时要查看构建, 点击 **<span class="inline-menu-item"><i class="fal fa-tasks"></i> BUILDS</span>**.

> 注意: Truffle 团队只会构建在存储库根的 rootfle 项目的存储库. 它在构建之前在根目录中寻找一个 <code>truffle-config.js</code> or <code>truffle.js</code> 配置 .阅读更多[配置文档](/docs/teams/reference/configuration#repository-structure).

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/starting-builds-01.png" alt="Build in progress" style="width: 100%">
</figure>

有关特定构建的更多详细信息, 随时单击列表中的任何构建的 **<span class="inline-button"><i class="far fa-clipboard-list-check"></i> BUILD DETAILS</span>**.

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/starting-builds-02.png" alt="Details of build in progress" style="width: 100%">
</figure>
