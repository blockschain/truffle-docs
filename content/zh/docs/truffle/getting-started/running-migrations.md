---
title: 运行迁移
weight: 4
---

迁移是JavaScript文件，可帮助您将合同部署到Ethereum网络. 
这些文件负责暂存部署任务，并在假设您的部署需求随时间变化时写入. 
随着项目的发展，您将创建新的迁移脚本，以进一步在区块链中的进展. 
先前运行迁移的历史记录通过特殊的`Migrations`合约，详细录制在链中.

## 命令

要运行迁移，请运行以下内容:

```shell
$ truffle migrate
```

这将运行项目`migrations`目录中的所有迁移。 
他们最简单, 迁移只是一组托管部署脚本。 
如果您的迁移以前成功运行, `truffle migrate` 将从运行的最后一个迁移开始执行, 仅运行新创建的迁移. 
如果没有新的迁移存在, `truffle migrate` 根本不会执行任何行动. 
你可以使用 `--reset` 选项从一开始运行所有迁移. 
记录了其他命令选项[此处](../reference/truffle-commands#migrate). 
对于本地测试，请务必在执行`truffle  migrate`之前配置和运行[Ganache](/ganache)等测试区块链. 
你也可以使用 `truffle develop`并运行迁移.


## 迁移档案

一个简单的迁移文件看起来像这样:

文档名称: `4_example_migration.js`

```javascript
var MyContract = artifacts.require("MyContract");

module.exports = function(deployer) {
  // deployment steps
  deployer.deploy(MyContract);
};
```

请注意，文件名以数字为前缀，并通过描述后缀. 
要记录迁移是否已成功进行编号的前缀。
后缀纯粹是为了人类可读性和理解。

### artifacts.require()

在迁移开始时，我们告诉Truffle我们希望通过`artifacts.require()`方法互动。
此方法类似于节点 `require`, 但在我们的情况下，它专门返回了我们可以在部署脚本的其余部分内使用的合同抽象. 
指定的名称应匹配在该源文件中 **合同定义的名称** . 
不要通过源文件的名称，因为文件可以包含多个合同.

考虑此示例，其中两个合同在同一源文件中指定:

文档名称: `./contracts/Contracts.sol`

```solidity
contract ContractOne {
  // ...
}

contract ContractTwo {
  // ...
}
```

只使用 `ContractTwo`, 你的 `artifacts.require()` 声明看起来像这样:

```javascript
var ContractTwo = artifacts.require("ContractTwo");
```

使用两份合同, 你需要两个 `artifacts.require()` 陈述:

```javascript
var ContractOne = artifacts.require("ContractOne");
var ContractTwo = artifacts.require("ContractTwo");
```

### module.exports

所有迁移都必须通过语法`module.exports`导出函数. 
每个迁移导出的函数应接受一个`deployer`对象作为其第一个参数. 
此对象通过提供清晰的语法来部署到部署智能合同以及执行一些部署更平凡的职责，例如保存部署的工件以供以后使用。 
`deployer`对象是用于分期部署任务的主界面，其API将在本页底部进行描述。

您的迁移功能也可以接受其他参数。请参阅下面的示例。

## 初始迁移

Truffle要求您有迁移合同才能使用迁移功能。 
本合同必须包含特定的界面，但您可以随意编辑此合同。 
对于大多数项目，本合同最初将作为第一次迁移部署，并且不会再次更新。 
使用`truffle init`创建新项目时，您还将默认收到此合同.

文档名称: `contracts/Migrations.sol`

```solidity
pragma solidity ^0.4.8;

contract Migrations {
  address public owner;

  // A function with the signature `last_completed_migration()`, returning a uint, is required.
  uint public last_completed_migration;

  modifier restricted() {
    if (msg.sender == owner) _;
  }

  function Migrations() {
    owner = msg.sender;
  }

  // A function with the signature `setCompleted(uint)` is required.
  function setCompleted(uint completed) restricted {
    last_completed_migration = completed;
  }

  function upgrade(address new_address) restricted {
    Migrations upgraded = Migrations(new_address);
    upgraded.setCompleted(last_completed_migration);
  }
}
```

您必须在第一次迁移内部部署此合同，以便利用迁移功能。  
默认情况下，在创建带有`truffle init`的新项目时提供以下迁移:

文档名称: `migrations/1_initial_migration.js`

```javascript
var Migrations = artifacts.require("Migrations");

module.exports = function(deployer) {
  // Deploy the Migrations contract as our only task
  deployer.deploy(Migrations);
};
```

从这里，您可以使用越来越多的数字前缀创建新的迁移来部署其他合同并执行进一步的部署步骤。

## 部署者

您的迁移文件将使用deployer段落部署任务。 
因此，您可以同步编写部署任务，并且它们将以正确的顺序执行:

```javascript
// Stage deploying A before B
deployer.deploy(A);
deployer.deploy(B);
```

或者，部署器上的每个功能都可以用作承诺，以队到取决于上一个任务的执行的部署任务:

```javascript
// Deploy A, then deploy B, passing in A's newly deployed address
deployer.deploy(A).then(function() {
  return deployer.deploy(B, A.address);
});
```

如果您发现语法更清晰，则可以将您的部署写为单个承诺链。Deployer API在本页底部讨论。

## 网络注意事项

可以根据部署到的网络条件地运行部署步骤。 
这是一个高级功能, 因此，请先在继续之前先查看[网络](/docs/advanced/networks)部分。

要有条件阶段部署步骤，请写下您的迁移，以便它们接受第二个参数, 叫 `network`. 例子:

```javascript
module.exports = function(deployer, network) {
  if (network == "live") {
    // Do something specific to the network named "live".
  } else {
    // Perform a different step otherwise.
  }
}
```

## 可用帐户

迁移也通过了Ethereum客户端和Web3提供商为您提供的帐户列表, 为您在部署期间使用. 
这是`web3.eth.getAccounts()`返回的完全相同的帐户列表.

```javascript
module.exports = function(deployer, network, accounts) {
  // Use the accounts within your migrations.
}
```

## deployer API

Deployer包含许多可用的功能，可简化您的迁移.

### deployer.deploy(contract, args..., options)

部署由合同对象指定的特定合同，具有可选的构造函数参数。 
这对Singleton合同非常有用，从而仅为您的DAPP存在一个本合同实例。 
这将在部署后设置合同的地址 (i.e., `Contract.address`将等于新已部署的地址), 它将覆盖存储的任何先前的地址.

您可以选择传递一系列合同或数组数组，以加快部署多个合约. 
此外，最后一个参数是一个可选的对象，可以包括名为`overwrite`的密钥以及其他交易参数，如 `gas` 和 `from`. 
如果 `overwrite` 被设定为 `false`, 如果已经部署了，则部署器不会部署此合同. 
这对于通过外部依赖性提供合同地址的某些情况是有用的.

请注意，您需要部署和链接任何库的合同在调用`deploy`之前首先取决于您的合同. 
有关更多详细信息，请参阅下面的`link`功能.

有关更多信息，请参阅[@truffle/contract](https://github.com/trufflesuite/truffle/tree/master/packages/contract)文档。


例子:

```javascript
// Deploy a single contract without constructor arguments
deployer.deploy(A);

// Deploy a single contract with constructor arguments
deployer.deploy(A, arg1, arg2, ...);

// Don't deploy this contract if it has already been deployed
deployer.deploy(A, {overwrite: false});

// Set a maximum amount of gas and `from` address for the deployment
deployer.deploy(A, {gas: 4612388, from: "0x...."});

// Deploying multiple contracts as an array is now deprecated.
// This used to be quicker than writing three `deployer.deploy()` statements as the deployer
// can perform the deployment as a single batched request.
// deployer.deploy([
//   [A, arg1, arg2, ...],
//   B,
//   [C, arg1]
// ]);

// External dependency example:
//
// For this example, our dependency provides an address when we're deploying to the
// live network, but not for any other networks like testing and development.
// When we're deploying to the live network we want it to use that address, but in
// testing and development we need to deploy a version of our own. Instead of writing
// a bunch of conditionals, we can simply use the `overwrite` key.
deployer.deploy(SomeDependency, {overwrite: false});
```

### deployer.link(library, destinations)

将已部署的库链接到合同或多个合同。 
`destinations` 可以是单一合同或多个合同数组. 
如果目的地内的任何合同不依赖于挂钩的库，则将忽略合同。

例子:

```javascript
// Deploy library LibA, then link LibA to contract B, then deploy B.
deployer.deploy(LibA);
deployer.link(LibA, B);
deployer.deploy(B);

// Link LibA to many contracts
deployer.link(LibA, [B, C, D]);
```

### deployer.then(function() {...})

就像一个承诺一样，运行任意部署步骤。 
在迁移期间使用此选项可调用特定的合同函数以添加，编辑和重新组织合同数据。

例子:

```javascript
var a, b;
deployer.then(function() {
  // Create a new version of A
  return A.new();
}).then(function(instance) {
  a = instance;
  // Get the deployed instance of B
  return B.deployed();
}).then(function(instance) {
  b = instance;
  // Set the new instance of A's address on B via B's setA() function.
  return b.setA(a.address);
});
```
