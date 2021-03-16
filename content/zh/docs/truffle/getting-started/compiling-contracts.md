---
title: 编译合约
weight: 3
---

## 位置

您的所有合约都位于您的项目`contracts/`目录中。
由于合约写入[巩固](https://solidity.readthedocs.io/en/develop/), 所有包含合约的文件的文件扩展名均为`.sol`.
关联的 Solidity [库](http://solidity.readthedocs.org/en/latest/contracts.html#libraries)也将具有`.sol`扩展名。

裸露的 Truffle [项目](/docs/truffle/quickstart) (通过 `truffle init` 创建), 您将获得一个`Migrations.sol`文件，该文件可帮助您进行部署.
如果您使用的是[ Truffle 盒](/boxes), 您将在此处拥有多个文件.

## 命令

要编译 Truffle 项目，请更进入项目所在目录的根目录，然后在终端中键入以下内容:

```shell
truffle compile
```

第一次运行时，将编译所有合约。
在随后的运行中，Truffle 将仅编译自上次编译以来已更改的合约。
如果您想覆盖此行为，请使用 `--all` 选项运行上述命令。

## 构建文物

您的编译工件将放置在`build/contracts/`目录中, 相对于您的项目根目录. (如果该目录不存在，则将创建它。)
生成的工件`.json`文件的名称**不反映** **源文件的名称**，而是**合约定义的名称**。
这意味着更改 `artifacts.require` 方法里面合约名称字符串匹配源文件的源可能会导致一个 `Error: Could not find artifacts for {yourContract} from any sources` 如果包含的智能合约定义是不同的.

这些工件是整体的 Truffle 内部工作, 他们在成功部署申请时发挥着重要组成部分.
**您不应该编辑这些文件** 因为它们将被合约编译和部署覆盖.

## 依存关系

您可以使用 Solidity [import](http://solidity.readthedocs.org/en/latest/layout-of-source-files.html#importing-other-source-files) 命令声明合约依赖项.
Truffle 将以正确的顺序编译合约，并确保所有依赖项都发送到编译器.
依赖关系可以用两种方式指定:

### 通过文件名导入依赖项

要从单独的文件导入合约，请将以下代码添加到您的 Solidity 源文件中:

```solidity
import "./AnotherContract.sol";
```

这将使所有合约在`AnotherContract.sol`中。
这里, `AnotherContract.sol` 相对于当前合约的路径是写的.

请注意，Solidity 允许其他导入语法.
欲获得更多信息看看 Solidity [import 文档](http://solidity.readthedocs.org/en/latest/layout-of-source-files.html#importing-other-source-files) .

### 从外部包导入合约

Truffle 支持通过[ethpm](/docs/truffle/getting-started/package-management-via-ethpm)和[NPM](/docs/truffle/getting-started/package-management-via-npm)安装的依赖项.
要从依赖项导入合约，请使用以下语法

```solidity
import "somepackage/SomeContract.sol";
```

这里, `somepackage` 表示通过 ethpm 或 npm 安装的包, 和 `SomeContract.sol` 表示该包提供的 Solidity 源文件.

请注意，在搜索从 NPM 安装的软件包之前，Truffle 首先将从 Ethpm 搜索已安装的软件包, 因此，在罕见的命名冲突中，将使用通过 ethpm 安装的包装.

有关如何使用 Truffle 的包管理功能的详细信息, 请看 Truffle [EthPM](/docs/truffle/getting-started/package-management-via-ethpm) and [NPM](/d和/truffle/getting-started/package-management-via-npm) 文档.
