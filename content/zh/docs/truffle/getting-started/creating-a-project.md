---
title: 创建一个项目
weight: 2
---

要使用大多数Truffle命令，您需要将它们运行它们针对现有的Truffle项目。
因此，第一步是创建一个Truffle项目。

您可以创建一个裸露的项目模板，但对于那些刚刚入门，您可以使用[松露盒](/boxes), 这是示例应用程序和项目模板. 
我们将使用[MetaCoin框](/boxes/metacoin), which create创建一个可以在账户之间转移的令牌

1. 为您的Truffle项目创建一个新目录:

   ```shell
   mkdir MetaCoin
   cd MetaCoin
   ```

2. 下载 ("unbox") 这 MetaCoin box:

   ```shell
   truffle unbox metacoin
   ```
   
   <p class="alert alert-info">
   <strong>Note</strong>: 您可以使用 `truffle unbox <box-name>` 命令下载任何其他 <a href="/boxes">Truffle Boxes</a>.
   </p>

   <p class="alert alert-info">
   <strong>Note</strong>: 创建不包含智能合约的裸露松露项目, use `truffle init`.使用
   </p>

   <p class="alert alert-info">
   <strong>Note</strong>: 即使它包含其他文件或目录
   您可以使用可选 `--force` 在当前目录中初始化项目，无论其状态如何 (e.g.即使它包含其他文件或目录). 
   这既适用于 `init` 和 `unbox` 命令. 
   请注意，这可能会覆盖目录中存在的文件。
   </p>

完成此操作后，您现在可以使用以下项目具有项目结构:

* `contracts/`: [实体合同](/docs/truffle/getting-started/interacting-with-your-contracts)目录
* `migrations/`: [可脚本化的部署文件](/docs/truffle/getting-started/running-migrations#migration-files)目录
* `test/`: 用于测试文件的目录[测试您的应用程序和合同](/docs/truffle/testing/testing-your-contracts)
* `truffle-config.js`: 松露[配置文件](/docs/truffle/reference/configuration)
