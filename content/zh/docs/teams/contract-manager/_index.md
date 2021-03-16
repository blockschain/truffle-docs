---
title: 合约管理者概述
linkTitle: 合约管理员
weight: 9
---

合约管理员提供了一个用户友好的界面，用于与您部署的合约实例进行交互。
它使您可以查看合约的当前状态并与合约功能进行交互。

<figure class="screenshot">
  <img class="img-fluid" src="/img/docs/teams/contract-manager-01.png" title=" Truffle 队合约经理视图" alt=" Truffle 队合约经理视图" />
  <figcaption class="text-center">管理合约</figcaption>
</figure>

注意: 当前，合约管理器是我们的 Early Access 计划的一部分，该程序启用后，您就可以访问尖端的和可能不稳定的功能。
它需要选择加入；单击侧边栏中的用户名或 GitHub 头像，导航至您的帐户设置。
点击 ADVANCED 然后选择 Early Access.

## Getting started

要使用合约管理器，您必须具有已部署的合约实例。
如果您需要有关部署合约的帮助，请查看[创建部署](/docs/teams/deployments/creating-a-deployment)部分以了解更多信息。
Once you've deployed your contract, navigate to the **<span class="inline-menu-item"><i class="fal fa-parachute-box"></i>DEPLOYMENTS</span>** page, toggle to **TABLE** view, and select the deployment from your list of deployments.
On the chosen deployment page, under the **CONTRACTS** tab, you can chose a contract to interact with by clicking on **<span class="inline-button"><i class="far fa-pager"></i> MANAGE</span>**.

Once you've successfully navigated to the contract manager, you'll see two sections: **State** and **Functions**.
The **State** section provides a quick glance at all of the public state variables in your contract.
The **Functions** section allows you to interact with your deployed contract instance.
To learn more on how to interact with your public contract functions, take a look at the [Interacting with functions](/docs/teams/contract-manager/interacting-with-functions) section.
