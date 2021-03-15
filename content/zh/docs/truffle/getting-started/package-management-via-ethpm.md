---
title: 通过EthPM进行软件包管理
linkTitle: EthPM包管理
weight: 7
---

EthPM是新的为Ethereum[包注册表](https://www.ethpm.com/). 
它遵循 [ERC190 spec](https://github.com/ethereum/EIPs/issues/190) 用于发布和消耗智能合约包, 并获得了许多不同的Etereum开发工具的广泛支持. 
要展示我们的支持，我们已经将Etereum Package Registry Integry集成到Trotfle中.

## 安装套件

从ethpm安装包几乎可以简单地安装通过NPM的包。您可以简单地运行以下命令:

```shell
$ truffle install <package name>
```

您还可以在特定版本上安装包:

```shell
$ truffle install <package name>@<version>
```

像NPM一样，ethpm版本跟随[semver](http://semver.org/). 
您可以在[Ethereum Package Registry](http://explorer.ethpm.com/)中找到所有可用软件包的列表.

## 安装依赖项

您的项目可以定义一个`ethpm.json`文件，其中包含将您的项目引入特定的依赖关系和版本。 
安装在“ethpm.json`文件中列出的所有依赖项，运行:

```shell
$ truffle install
```

有关`ethpm.json`文件的更多详细信息，请参阅下面的[包配置](/docs/getting_started/packages-ethpm#package-configuration)。

## 消耗已安装的合约

安装的包裹将放在项目文件夹 `installed_contracts` 目录中. 如果 `installed_contracts` 目录不存在它会为你创造. 
您应该将此文件夹视为您使用NPM处理`node_modules`文件夹 -- 也就是说，除非你知道你在做什么，否则你不应该编辑内容. :)

已安装的软件包可以在您的测试，迁移和稳定性合约文件中消费 通过 `import`'ing 或 `require`'ing 按名称包裹和合约. 
例如, 以下 Solidity 合约将导入来自 `owned` 包的 `owned.sol` 文件 :

```solidity
pragma solidity ^0.4.2;

import "owned/owned.sol";

contract MyContract is owned {
  // ...
}
```

相似地, 以下迁移文件将使用来自`ex`包合约 `ENS.sol` :

文件: `./migrations/2_deploy_contracts.js`

```javascript
var ENS = artifacts.require("ens/ENS");
var MyContract = artifacts.require("MyContract");

module.exports = function(deployer) {
  // Only deploy ENS if there's not already an address already.
  // i.e., don't deploy if we're using the canonical ENS address,
  // but do deploy it if we're on a test network and ENS doesn't exist.
  deployer.deploy(ENS, {overwrite: false}).then(function() {
    return deployer.deploy(MyContract, ENS.address);
  });
};
```

注意在上面的迁移中, 我们消耗`ENS`包并根据是否已有地址集. 
这是[部署](/docs/getting_started/migrations#deployer-deploy-contract-args-options-)提供给您的奇特技巧这使得编写迁移的更容易依赖于网络伪影的存在更容易. 
在这种情况下, 如果我们在Ropsten网络上运行我们的迁移, 这个迁移 **不会** 部署 `ENS` 合约 因为 (在这种写作时) Ropsten是规范的 `ENS` 合约 存在 -- 我们不想部署自己的部署. 
但如果我们正在运行我们对不同网络的迁移, 或者测试网络也许, 然后我们想部署 `ENS` 合约 因此，我们有一个依赖合约来合作.

## 发布自己的包

发布您自己的包是直截了当的，但像NPM一样，需要更多配置。

### Ropsten，Ropsten，Ropsten

Ethereum Package Registry目前存在于Ropsten测试网络上。 
要发布到注册表，我们需要设置自己的Ropsten配置，因为我们将进行需要签名的交易。

在此示例中，我们将使用Infura与`Truffle-Hdwallet-Provider` NPM模块一起发布包和一个12字的HD-wallet助记符，代表了罗特伦网络上的Ethereum地址. 
首先，通过项目目录中的NPM安装`Truffle-Hdwallet-Provider`:

```shell
$ npm install truffle-hdwallet-provider --save
```

然后编辑配置以使用12字助记符添加`ropsten`网络:

File: `truffle.js`

```javascript
var HDWalletProvider = require("truffle-hdwallet-provider");

// 12-word mnemonic
var mnemonic = "opinion destroy betray ...";

module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*" // Match any network id
    },
    ropsten: {
      provider: () =>
        new HDWalletProvider(mnemonic, "https://ropsten.infura.io/v3/YOUR-PROJECT-ID"),
      network_id: 3 // official id of the ropsten network
    }
  }
};
```

### 套餐配置

与NPM一样，ethpm的配置选项转入一个名为`ethpm.json`的单独的JSON文件。 
此文件与Truffle配置搭配，并块块块发布包的所有信息。 
您可以在[配置](/docs/advanced/configuration)部分中看到完整的可用选项列表。

文件: `ethpm.json`

```javascript
{
  "package_name": "adder",
  "version": "0.0.3",
  "description": "Simple contract to add two numbers",
  "authors": [
    "Tim Coulter <tim.coulter@consensys.net>"
  ],
  "keywords": [
    "ethereum",
    "addition"
  ],
  "dependencies": {
    "owned": "^0.0.1"
  },
  "license": "MIT"
}
```

### 命令

确认配置后，发布是一个捕捉：

```shell
$ truffle publish
```

您将看到类似于下面的输出，确认您的包已成功发布。

```shell
$ truffle publish
Gathering contracts...
Finding publishable artifacts...
Uploading sources and publishing to registry...
+ adder@0.0.3
```

### 发布之前

使用像默认设置为匹配的默认设置为匹配任何Ethereum客户端的网络时 (喜欢 [Ganache](/ganache) 或者 Truffle Develop), 你必然会有网络文物躺在那里你不想发布. 
在发布包之前，请考虑运行以下命令以删除任何无关的网络工件:

```shell
$ truffle networks --clean
```

有关更多信息，请参阅[命令参考](/docs/advanced/commands#networks) 。
