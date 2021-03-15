---
title: Ethereum工作区概述
linkTitle: 工作区
weight: 2
---

## 主界面

创建工作区后，屏幕将显示有关服务器的一些详细信息，并列出许多帐户。
**每个账户有 100 以太币**.
在所有帐户中自动拥有以太币使您可以专注于开发应用程序.

![Ganache](/img/docs/ganache/ganache-accounts.png)

<p class="text-center">*本地帐户*</p>

共有六页:

- **Accounts** 显示生成的帐户及其余额. This is the default view.
- **Blocks** 显示在区块链上开采的每个区块以及使用的天然气和交易.
- **Transactions** l 禁止所有交易针对区块链.
- **Contracts** 列出工作区的 Truffle 项目中包含的合同. For more information on how Ganache handles contracts, see our [Contracts Page documentation](/docs/ganache/truffle-projects/contracts-page).
- **Events** 列出自此工作区创建以来已触发的所有事件. Ganache will attempt to decode events triggered by contracts in your Truffle project. For more information on events, see our [Events Page documentation](/docs/ganache/truffle-projects/events-page).
- **Logs** 显示服务器的日志，这对于调试非常有用.

另请注意，您可以从顶部的搜索框中搜索区块编号或交易哈希.

## 您已启动并正在运行！

本指南让您开始使用零配置的个人以太坊开发区块链. 如果您有一个现有的 Truffle 项目，希望在此工作空间中跟踪其合同和事件，请查看[链接 Truffle 项目文档](/docs/ganache/truffle-projects/linking-a-truffle-project).
如果您只需要自定义一些选项并保存此工作区以供以后使用，请查看[创建工作区文档](/docs/ganache/workspaces/creating-workspaces#saving-the-current-quickstart-blockchain-as-a-new-workspace).
