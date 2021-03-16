---
title: Ganache设置
weight: 1
---

您可以通过`设置`页面更改生成的区块链的某些功能, 通过右上角的齿轮图标访问.
创建[新工作区](/docs/ganache/workspaces/creating-workspaces)时，系统也会提示您设置屏幕.

![访问Ganache设置](/img/docs/ganache/ganache-settings-gear-icon.png)

<p class="text-center">*访问Ganache设置*

我们已将设置分为几页:

- **Workspace** 设置工作空间名称并显示当前链接的 Truffle 或 Corda 项目。 有关更多信息，请参见有关[创建](/docs/ganache/workspaces/creating-workspaces)和[删除](/docs/ganache/workspaces/deleting-workspaces)工作区的更详细的文档。.
- **Ethereum**
  - **Server** 显示有关网络连接的详细信息，包括主机名，端口，网络 ID 以及是否自动将每个事务挖掘到一个块中。
  - **Accounts & Keys** 设置有关创建的帐户数以及使用特定助记符还是让 Ganache 生成自己的助记符的详细信息。
  - **Chain** 为生成的区块链的起源和参数设置配置详细信息，包括天然气限额和天然气价格。
  - **Advanced** 切换 Google Analytics（分析），这对于 Ganache 团队跟踪应用程序的使用非常有用。
- **Corda**
  - **Nodes** 管理网络的节点。
  - **Notaries** 管理网络的公证人。
  - **Advanced** 设置默认的 PostgreSQL 端口并切换 Google Analytics（分析），这对于团队根据匿名使用情况指标改进 Ganache 很有用。
- **About** 包含有关当前安装的 Ganache 版本的信息，以及指向我们网站和[Ganache GitHub 存储库](https://github.com/trufflesuite/ganache)的链接。.

进行更改后，您将必须在应用程序上单击**Restart**以使更改生效。

![Ganache设置](/img/docs/ganache/ganache-settings.png)

<p class="text-center">*Ganache设置*

## 配置 Truffle 连接到 Ganache

要配置 Truffle 连接到 Ganache，请编辑`truffle-config.js`以指向 Ganache 的 IP 和端口，例如

```
module.exports = {
  networks: {
    development: {
      host: "localhost",
      port: 7545,
      network_id: "1234"
    }
    // live: { ... }
  }
};
```

然后，您可以运行这样的`truffle migrate --network development`迁移命令.
