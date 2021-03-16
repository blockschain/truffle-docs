---
title: 快速开始
weight: 2
---

此页面将带您通过创建 Truffle Teams 帐户的基础知识，并将其链接到 Truffle 项目存储库。

> 注意: 在开始之前，请确保您有一个包含块状项目的 GitHub 存储库。

## 创建一个帐户

开始, 导航[https://my.truffleteams.com](https://my.truffleteams.com).

点击 **<span class="inline-button"><i class="fab fa-github"></i> LOGIN WITH GITHUB</span>**.
如果您尚未登录您的 GitHub 帐户，Github 会提示您这样做。

如果您是您的个人帐户以外的任何组织的成员，系统将提示您选择 ORG 以继续安装。
使用现有 Truffle Teams 安装的组织将有一个 **Configure >** 链接。

![Truffle团队数据视图](/img/docs/teams/install-01.png)

接下来，您将被要求许可 Truffle 团队链接到一个或多个 GitHub 存储库。
选择要添加的存储库，然后单击`continue`。
选择任一个 **All repositories** 将此 account/org 中的所有 Repos 添加到团队中或者 **仅选择存储库** 从下拉列表中选择单个 REPOS.

注意: 我们可以随时在必要时添加回购。 更多信息请看[添加存储库](/docs/teams/getting-started/adding-repositories)文档.

最后, 点击 **Install** 在所选存储库上安装 Troofle 团队.

<p class="alert alert-warning">
为什么我们需要某些权限？ 请看 [权限披露](/docs/teams/reference/permissions-disclosure) 部分 完全分解为什么我们要求每次许可.

![Truffle Teams DATA view](/img/docs/teams/install-03.png)

然后我们到达主屏幕，看看我们添加的 Repos - 让我们提交一些代码，看看 Truffle 团队如何自动运行我们的测试！

## 开始构建

一旦将新提交被推送到添加到 Truffle 团队的存储库的任何分支，构建将自动启动。
您将在`BUILDS`页面上的 Truffle 团队接口和 COMMIT 上看到 Quite out 的构建。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/starting-builds-comp.png" alt="在块菌团队和GitHub中建立进展" style="width: 100%">
</figure>

## 部署合约

请参阅我们的详细教程, ["学习用 Truffle 团队部署"](https://www.trufflesuite.com/tutorials/learn-how-to-deploy-with-truffle-teams).

## 继续学习

这款 Quickstart 向您展示了 Truffle 团队测试工作流程的基础知识，但一旦部署了您的合约，就会更多地了解 **[监控部署合约](/docs/teams/deployments/contract-monitoring)**.

我们在快速发展的循环中;不断添加新功能和精炼现有功能。如果您遇到任何故障或错误，请在[ Truffle 团队 GitHub 存储库](https://github.com/trufflesuite/truffle-teams/issues)上提出问题.
要收到最新更新的通知，请考虑[注册 Truffle 团队邮件列表](https://share.hsforms.com/1OaTglVhGTdWk7spR6nE_AA34pbp).
