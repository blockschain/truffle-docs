---
title: 创建一个项目
weight: 2
---

要使用大多数 Truffle 命令，您需要将它们运行它们针对现有的 Truffle 项目。
因此，第一步是创建一个 Truffle 项目。

您可以创建一个裸露的项目模板，但对于那些刚刚入门，您可以使用[ Truffle 盒](/boxes), 这是示例应用程序和项目模板.
我们将使用[MetaCoin 框](/boxes/metacoin), which create 创建一个可以在账户之间转移的令牌

1. 为您的 Truffle 项目创建一个新目录:

   ```shell
   mkdir MetaCoin
   cd MetaCoin
   ```

2. 下载 ("unbox") 这 MetaCoin box:

   ```shell
   truffle unbox metacoin
   ```

   注意: 您可以使用 `truffle unbox <box-name>` 命令下载任何其他 [Truffle Boxes](/boxes).

   注意: 创建不包含智能合约的裸露 Truffle 项目, use `truffle init`.使用

   注意: 即使它包含其他文件或目录
   您可以使用可选 `--force` 在当前目录中初始化项目，无论其状态如何 (e.g.即使它包含其他文件或目录).
   这既适用于 `init` 和 `unbox` 命令.
   请注意，这可能会覆盖目录中存在的文件。

完成此操作后，您现在可以使用以下项目具有项目结构:

- `contracts/`: [实体合约](/docs/truffle/getting-started/interacting-with-your-contracts)目录
- `migrations/`: [可脚本化的部署文件](/docs/truffle/getting-started/running-migrations#migration-files)目录
- `test/`: 用于测试文件的目录[测试您的应用程序和合约](/docs/truffle/testing/testing-your-contracts)
- `truffle-config.js`: Truffle [配置文件](/docs/truffle/reference/configuration)
