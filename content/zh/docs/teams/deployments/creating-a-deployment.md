---
title: 创建部署
weight: 1
---

目前，Truffle 团队支持以 Ethereum Testnets，Ethereum Mainnet 和[Sandboxes](/docs/teams/sandboxes/sandboxes-overview)的部署，随着时间的推移，支持更多目标网络。

根据您为 **<span class="inline-menu-item"><i class="fal fa-parachute-box"></i>DEPLOYMENTS</span>** 页面选择的视图略有不同，创建部署略有不同。
一般过程如下:

1. [选择提交部署](#choose-a-commit-to-deploy)
2. [选择网络并连接钱包](#select-network-and-connect-wallet)
3. [选择一个部署上下文](#select-a-deployment-context)
4. [开始部署](#start-deployment)
5. [完成部署](#finalize-deployment)

## 选择要部署的提交

此步骤可能会略有不同，具体取决于您所使用的部署视图， [cards](#cards-view) 或者 [table](#table-view).

### 卡视图

要开始部署，请在您要部署的版本上按 **<span class="inline-button">DEPLOY <i class="far fa-parachute-box"></i></span>** .
您也可以点击 **<span class="inline-button"><i class="fas fa-rocket"></i> NEW DEPLOYMENT</span>**.
部署向导模式将弹出，并引导您完成部署过程。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/commit-card.png" alt="Commit Card">
</figure>

### 表格检视

对于 **TABLE** 视图，您将从部署向导中选择要部署的内部版本。
ˇ **<span class="inline-button"><i class="fas fa-rocket"></i> NEW DEPLOYMENT</span>**, 这将打开部署向导模式。
从 **Build to Deploy** 下拉列表中，选择要部署的内部版本。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/table-view-deployment-wizard.png" alt="Table view deployment wizard">
  <figcaption class="text-center font-italic">部署向导</figcaption>
</figure>

## 选择网络并连接钱包

在部署向导中，选择一个 **Destination Network**, 如果您的钱包已经设置好，则可以转到[选择部署上下文](#select-a-deployment-context) step.
如果尚未设置您的钱包，则可以查看并单击 **<span class="inline-button">CONNECT WALLET</span>** 按钮。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/select-network-connect-wallet.png" alt="Deployment wizard modal">
  <figcaption class="text-center font-italic">部署向导</figcaption>
</figure>

MetaMask 将弹出，要求您登录（如果尚未登录）。
然后，您需要按 **Connect** 以确认与 Truffle Teams 的连接。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/metamask-connect.png" alt="Deployment wizard modal and MetaMask connect pop-up" style="width:100%">
</figure>

如果向导没有更改（即您没有看到开始部署的按钮），则可能需要将 MetaMask 网络切换到目标网络。这可能会重新加载页面；如果发生这种情况，则需要重复上述步骤。

![MetaMask Network](/img/tutorials/learn-how-to-deploy-with-truffle-teams/metamask-network.png)

在继续之前，请确保您已在 MetaMask 中选择了正确的帐户。

![MetaMask Account](/img/tutorials/learn-how-to-deploy-with-truffle-teams/metamask-account.png)

## 选择部署上下文

现在，您应该看到向导提示您输入“部署上下文”。
将其设置为**Create a New Deployment **，或选择以前的部署进行迁移。

<i class="far fa-info-circle"></i> 部署环境: 通过此选项，您可以在要使用其部署的工件的同一网络上选择一个现有的部署。
Truffle 支持迁移应用程序的概念，并且只会从上次部署（也称为部署上下文）运行新的迁移脚本。
这在少数情况下变得很有用：也许您添加了额外的合约以与现有部署一起使用，您的 Truffle 项目使用代理合约来升级您的合约，等等。
从技术上讲，选择“部署上下文”将在运行“ Truffle 迁移”之前将 Truffle 工件从您在目录中选择的部署上下文中放入。

## 开始部署

现在，您应该可以看到并单击 **<span class="inline-button">OK, START DEPLOYING</span>** 开始部署了！

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/deployment-wizard-ready.png" alt="Deployment wizard modal ready">
</figure>

<p class="alert alert-warning">
<i class="far fa-exclamation-triangle"></i> Be Aware: 从这里开始，不要关闭选项卡，刷新页面或断开网络连接，这一点很重要。
我们正在努力提供更强大的体验，使您能够选择尚未完成的部署，但是就目前而言，我们的当前版本要求该选项卡保持打开和连接状态。

Truffle 团队只能同时处理这么多部署，因此您可能会看到部署已排队。
您必须等待（不关闭/刷新选项卡）部署才能显示在列表的最前面。
但是，我们正在努力使这种体验更加顺畅。

部署开始处理后，您将看到 Truffle Teams 为准备部署所做的步骤清单。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/deployment-wizard-preparation.png" alt="Deployment wizard preparation steps modal">
</figure>

准备步骤完成后，您将看到一个屏幕，其中包含正在处理的迁移列表。
您还应该从 MetaMask 弹出一个用于您的第一笔交易的弹出窗口。

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/deployment-wizard-first-tx.png" alt="Deployment wizard first transaction modal">
</figure>

您会注意到，此与 MetaMask 的接口就像将事务发送到任何其他 dapp。
发送此交易的是您的帐户，您可以完全控制它。
此外，我们强烈建议您将 **GAS FEE** 更改为更高，以便您的交易运行更快。
对于像 Ropsten 这样的测试网，始终选择**快速**选项是可以承受的。

![MetaMask Gas](/img/tutorials/learn-how-to-deploy-with-truffle-teams/metamask-gas.png)

对交易汽油费满意后，请按**确认**发送交易。交易确认后（MetaMask 和 Truffle 团队确认的时间可能会稍有偏移），您将收到下一笔交易。重复此过程，直到看到一条消息，您的部署已完成。

## 完成部署

稍等片刻后，您将看到一个窗口，其中包含您的部署结果：

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/deployment-wizard-results.png" alt="Deployment wizard results modal">
</figure>

您的合约已部署！那很简单。
继续并在向导中按 **<span class="inline-button">GREAT! GO BACK TO WORKFLOW</span>** 或 **X**。
如果您使用的是“ CARDS”视图，现在应该在“ Staging”列中看到一张新卡。
如果您使用的是 **TABLE** 视图，则新的部署将出现在第一行中。有关更多信息，请查看我们文档的[Deployment details](/docs/teams/deployments/deployment-details)部分。
