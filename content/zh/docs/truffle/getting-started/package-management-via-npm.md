---
title: 通过NPM包管理
linkTitle: NPM包管理
weight: 8
---

Truffle 带有`npm`集成标准, 如果存在，则会知道项目中的`node_modules`目录.
这意味着您可以通过“NPM”使用和分发启用合约，DAPP 和 Ethereum 的库，使您的代码提供给其他人和其他可用的代码。

## 包装布局

默认情况下，使用 Truffle 创建的项目具有特定的布局，使它们能够用作包。
这种布局是不需要的，但如果用作公共约定 -- or "de-facto standard" -- 然后通过 NPM 分发合约和 DAPP 将变得更加容易.

Truffle 套餐中最重要的目录是以下内容:

- `/contracts`
- `/build` (which includes `/build/contracts`, created by Truffle)

第一个目录是您的合约目录，包括您的原始巩固合约。
第二个目录是构建目录，更具体地 `/build/contracts`, 其中以`.json`文件”形式构建文物.
包括您包中的原始合约将允许其他人在自己的稳固码内导入这些合约。
同样，包括您的包装中的`.JSON`构建文物将允许其他人与 JavaScript 的合约无缝互动，可用于 DAPP，脚本和迁移。

## 使用包装

在您自己的项目中使用包时, 值得注意的是，有两个地方可能有兴趣使用其他合约代码: 在您的合约中以及在 JavaScript 代码中 (迁移和测试).
以下提供了每个案例的示例，并讨论了使最多的其他合约和构建文物的技术。

### 正在安装

对于此示例，我们将使用[示例 Truffle Library](https://github.com/ConsenSys/example-truffle-library),它提供了部署到 Morden 测试网络的简单名称注册表.
为了将其用作依赖项，我们必须首先通过`npm`将其安装在我们的项目中:

```shell
$ cd my_project
$ npm install example-truffle-library
```

请注意，上面的最后一个命令下载包并将其放在`my_project / node_modules`目录中， 这对于以下示例非常重要.
有关使用`NPM`安装包的帮助，请参阅[NPM 文档](https://docs.npmjs.com/)。

### 在您的合约范围内

要在合约中使用包裹的合约，这可以像稳定性一样简单[导入](http://solidity.readthedocs.io/en/develop/layout-of-source-files.html?#importing-other-source-files)声明。
当您的导入路径不是[显式相对或绝对]时(/docs/getting_started/compile#dependencies), 这意味着块块您正在寻找特定命名包的文件.
考虑使用上面提到的示例 Truffle 库的示例:

```solidity
import "example-truffle-library/contracts/SimpleNameRegistry.sol";
```

由于路径没有以`./`, Truffle 知道要查看您的项目的`node_modules`目录，适用于`example-truffle-library`文件夹.
从那里，它解决了为您提供您要求的合约的路径.

### 在 JavaScript 代码中

在 JavaScript 代码中与包裹的合约互动, 你只是需要 `require` 那个包装 `.json` 文件, 然后使用 [@truffle/contract](https://github.com/trufflesuite/truffle/tree/master/packages/contract) 模块将这些转变为可用的抽象:

```javascript
var contract = require("@truffle/contract");
var data = require("example-truffle-library/build/contracts/SimpleNameRegistry.json");
var SimpleNameRegistry = contract(data);
```

要使用这些抽象，请参阅[与您的合约互动](/docs/getting_started/contracts)部分有关更多详细信息。

### 程序包的部署地址

有时您希望您的合约与包装以前部署的合约进行互动。
由于部署的地址存在于包的`.json`文件中，因此您必须执行额外的步骤以将这些地址达到合约。
为此，请使您的合约接受依赖合约的地址，然后使用迁移。
以下是项目中存在的示例合约以及示例迁移:

合约: `MyContract.sol`

```solidity
pragma solidity ^0.4.13;

import "example-truffle-library/contracts/SimpleNameRegistry.sol";

contract MyContract {
  SimpleNameRegistry registry;
  address public owner;

  function MyContract {
    owner = msg.sender;
  }

  // Simple example that uses the deployed registry from the package.
  function getModule(bytes32 name) returns (address) {
    return registry.names(name);
  }

  // Set the registry if you're the owner.
  function setRegistry(address addr) {
    require(msg.sender == owner);

    registry = SimpleNameRegistry(addr);
  }
}
```

移民: `3_hook_up_example_library.js`

```javascript
// Note that artifacts.require takes care of creating an abstraction for us.
var SimpleNameRegistry = artifacts.require(
  "example-truffle-library/SimpleNameRegistry"
);

module.exports = function (deployer) {
  // Deploy our contract, then set the address of the registry.
  deployer
    .deploy(MyContract)
    .then(function () {
      return MyContract.deployed();
    })
    .then(function (deployed) {
      return deployed.setRegistry(SimpleNameRegistry.address);
    });
};
```

### 发布之前

使用像默认`develop`网络这样的网络时这配置为匹配任何 Ethereum 客户端 (如 [Ganache](/ganache) 或 Truffle Develop), 你必然会有网络文物躺在那里你不想发布.
在发布包之前，请考虑运行以下命令以删除任何无关的网络工件:

```shell
$ truffle networks --clean
```

有关更多信息，请参阅[命令参考]。
