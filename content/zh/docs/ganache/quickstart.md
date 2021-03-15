---
title: Ganache 快速开始
linkTitle: 快速开始
weight: 1
---

本快速入门指南将引导您逐步安装 Ganache，并通过快速入门工作区创建个人开发区块链。

如果这不是您第一次使用 Ganache，或者您已经知道需要自定义配置选项，请查看[创建工作区文档](/docs/ganache/workspaces/creating-workspaces).

> 使用以太坊并且更喜欢使用命令行？: 该页面仅关注图形界面。 请参阅[Ganache CLI 自述文件](https://github.com/trufflesuite/ganache-cli/blob/master/README.md)，以获取有关 Ganache 命令行风格的更多信息。

## 1. 安装 Ganache

[下载](https://github.com/trufflesuite/ganache/releases) 适用于您的操作系统的版本:

- Windows: `Ganache-*.appx`
- Mac: `Ganache-*.dmg`
- Linux: `ganache-*.AppImage`

接下来，双击下载的文件，按照提示进行操作，然后就可以开始运行了。

<p class="alert alert-info">
<strong>Note</strong>: 首次启动Ganache时，系统会询问您是否要允许Google Analytics（分析）跟踪。尽管是可选的，但启用此选项将有助于开发团队更深入地了解如何使用Ganache。 此跟踪完全是匿名的，不会共享任何帐户数据或私钥。
</p>

## 2. 创建工作区

首次打开 Ganache 时，您会看到主屏幕。 在此屏幕上，系统提示您加载现有工作区（如果有），创建新的自定义工作区或使用[默认选项](/docs/ganache/reference/workspace-default-configuration)快速启动一键式区块链.
现在，让我们来看一个快速入门工作区。
从`QUICKSTART`下拉菜单中选择所需的区块链; 您可以选择启动以太坊节点或 Corda 网络，然后单击`QUICKSTART`按钮。

![空主屏幕](/img/docs/ganache/ganache-home-empty.png)

现在您已经创建了一个工作区，让我们看一下您可以做什么:

- **[以太坊工作区概述](./workspaces/ethereum)**
- **[Corda 工作区概述](./corda/workspace-overview)**
