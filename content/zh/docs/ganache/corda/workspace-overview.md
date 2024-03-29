---
title: Corda 工作区概述
linkTitle: 工作区概述
weight: 2
---

For Corda technical documentation not related to Ganache head over to [Corda's official documentation](https://docs.corda.net/docs/corda-os/4.4.html).

## 主界面

Once you've created a workspace, the screen will show some details about the nodes on the network.

![Ganache](/img/docs/ganache/corda/nodes.png)

<p class="text-center">*Corda Nodes*

There are five pages available:

- [**Nodes**](../corda/nodes) lists the nodes and notaries on the network.
- [**Transactions**](../corda/transactions) displays a list of all transactions
- [**CorDapps**](../corda/cordapps) lists all CorDapp jars installed on the network.
- [**Shell**](../corda/shell) provides Corda CRaSH shell access to each node and notary.
- **Logs** shows the logs for the Ganache server, nodes, and notaries, which is useful for debugging.

## 您已启动并正在运行！

This guide got you started with a zero-config personal Corda development network. If you have an existing CorDapp project whose CorDapp transactions you'd like tracked in this workspace, check out the [Linking a CorDapp Project documentation](/docs/ganache/corda/linking-a-corda-project). If you just need to customize some options and save this workspace for later, check out the [Creating Workspaces documentation](/docs/ganache/workspaces/creating-workspaces#saving-the-current-quickstart-blockchain-as-a-new-workspace).
