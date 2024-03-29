---
title: 快速开始
weight: 2
---

此页面将带您了解创建 Truffle 项目并将智能合约部署到区块链的基础知识。

> 注意: 在开始之前，请确保阅读我们的[Ethereum 概述](/tutorials/ethereum-overview)页

## 建立项目

您需要在现有的 Truffle 项目上运行大多数 Truffle 命令,因此第一步是创建一个 Truffle 项目。

您可以创建一个裸露的项目模板，但对于那些刚刚入门的可以使用[Truffle Boxes](/boxes), 这是一个示例应用程序和项目模板.
我们将使用[MetaCoin box](/boxes/metacoin), 创建一个可以在账户之间转移的令牌:

1. 为您的 Truffle 项目创建一个新目录:

   ```shell
   mkdir MetaCoin
   cd MetaCoin
   ```

2. 下载 ("unbox") MetaCoin box:

   ```shell
   truffle unbox metacoin
   ```

   > 注意: 您可以使用 `truffle unbox <box-name>` 命令下载任何其他 Truffle 盒.

   > 注意: 创建不包含智能合约的裸露 Truffle 项目, 使用 `truffle init`.

完成此操作后，您将拥有一个包含以下项目的项目结构:

- `contracts/`: [实体合约](/docs/truffle/getting-started/interacting-with-your-contracts)目录
- `migrations/`: [可脚本化的部署文件](/docs/truffle/getting-started/running-migrations#migration-files)的目录
- `test/`: 用于测试文件的目录[测试您的应用程序和合约](/docs/truffle/testing/testing-your-contracts)
- `truffle.js`: Truffle [配置文件](/docs/truffle/reference/configuration)

## 探索项目

> 注意: 该页面只是一个快速入门，因此我们在这里不再赘述。请参阅 Truffle 文档的其余部分以了解更多信息。

1. 在文本编辑器中打开 `contracts/MetaCoin.sol` 文件. 这是一个智能合约（以 Solidity 编写），可创建 MetaCoin 令牌。 请注意，这也引用了在同一目录中另一个 Solidity 文件 `contracts/ConvertLib.sol` .

2. 打开 `contracts/Migrations.sol` 文件. 这是一个单独的 Solidity 文件，用于管理和更新[已部署智能合约的状态](/docs/truffle/getting-started/running-migrations). 该文件随每个 Truffle 项目一起提供，通常不进行编辑.

3. 打开 `migrations/1_initial_migration.js` 文件. 该文件是在 Migrations.sol 文件中找到的 Migrations 合约的迁移（部署）脚本。

4. 打开 `migrations/2_deploy_contracts.js` 文件. 该文件是`MetaCoin`合约的迁移脚本。 (迁移脚本按顺序运行，因此以`2`开头的文件将在以`1`开头的文件之后运行。)

5. 打开 `test/TestMetacoin.sol` 文件. 这是一个[用 Solidity 编写的测试文件](/docs/truffle/testing/writing-tests-in-solidity) 这可以确保您的合约按预期工作。

6. 打开 `test/metacoin.js` 文件. 这是一个[用 JavaScript 编写的测试文件](/docs/truffle/testing/writing-tests-in-javascript) 执行与上面的 Solidity 测试类似的功能。

7. 打开 `truffle-config.js` 文件. 这是 Truffle [配置文件](/docs/truffle/reference/configuration), 用于设置网络信息和其他与项目相关的设置。该文件为空，但这没关系，因为我们将使用一些内置默认值的 Truffle 命令。

## 测验

1. 在终端上，运行 Solidity 测试:

   ```shell
   truffle test ./test/TestMetaCoin.sol
   ```

   您将看到以下输出

   ```sh
    TestMetacoin
      √ testInitialBalanceUsingDeployedContract (71ms)
      √ testInitialBalanceWithNewMetaCoin (59ms)

    2 passing (794ms)
   ```

   > 注意: 如果您使用的是 Windows，并且在运行此命令时遇到问题, 请参阅[有关解决 Windows 上命名冲突](/docs/truffle/reference/configuration#resolving-naming-conflicts-on-windows)的文档.

   这些树测试是根据合约运行的，并显示了有关测试应该执行的描述。

1. 运行 JavaScript 测试:

   ```shell
   truffle test ./test/metacoin.js
   ```

   您将看到以下输出

   ```sh
     Contract: MetaCoin
       √ should put 10000 MetaCoin in the first account
       √ should call a function that depends on a linked library (40ms)
       √ should send coin correctly (129ms)

     3 passing (255ms)
   ```

## 编译中

1. 编译智能合约:

   ```shell
   truffle compile
   ```

   您将看到以下输出:

   ```sh
   Compiling .\contracts\ConvertLib.sol...
   Compiling .\contracts\MetaCoin.sol...
   Compiling .\contracts\Migrations.sol...

   Writing artifacts to .\build\contracts
   ```

## 使用 Truffle Develop 进行迁移

> 注意: 使用 [Ganache](/ganache), 请跳到下一部分.

要部署我们的智能合约，我们将需要连接到区块链。
Truffle 具有内置的私有区块链，可用于测试。
该区块链在您的系统本地，并且不与主要的以太坊网络交互。

您可以使用[Truffle Develop](/docs/truffle/getting-started/using-truffle-develop-and-the-console#truffle-develop)创建此区块链并与之交互.

1. 运行 Truffle Develop:

   ```shell
   truffle develop
   ```

   您将看到以下信息:

   ```sh
   Truffle Develop started at http://127.0.0.1:9545/

   Accounts:
   (0) 0x627306090abab3a6e1400e9345bc60c78a8bef57
   (1) 0xf17f52151ebef6c7334fad080c5704d77216b732
   (2) 0xc5fdf4076b8f3a5357c5e395ab970b5b54098fef
   (3) 0x821aea9a577a9b44299b9c15c88cf3087f3b5544
   (4) 0x0d1d4e623d10f9fba5db95830f7d3839406c6af2
   (5) 0x2932b7a2355d6fecc4b5c0b6bd44cc31df247a2e
   (6) 0x2191ef87e392377ec08e7c08eb105ef5448eced5
   (7) 0x0f4f2ac550a1b4e2280d04c21cea7ebd822934b5
   (8) 0x6330a553fc93768f612722bb8c2ec78ac90b3bbc
   (9) 0x5aeda56215b167893e80b4fe645ba6d5bab767de

   Private Keys:
   (0) c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3
   (1) ae6ae8e5ccbfb04590405997ee2d52d2b330726137b875053c36d94e974d162f
   (2) 0dbbe8e4ae425a6d2687f1a7e3ba17bc98c673636790f1b8ad91193c05875ef1
   (3) c88b703fb08cbea894b6aeff5a544fb92e78a18e19814cd85da83b71f772aa6c
   (4) 388c684f0ba1ef5017716adb5d21a053ea8e90277d0868337519f97bede61418
   (5) 659cbb0e2411a44db63778987b1e22153c086a95eb6b18bdf89de078917abc63
   (6) 82d052c865f5763aad42add438569276c00d3d88a2d062d36b2bae914d58b8c8
   (7) aa3680d5d48a8283413f7a108367c7299ca73f553735860a87b08f39395618b7
   (8) 0f62d96d6675f32685bbdb8ac13cda7c23436f63efbb9d07700d8669ff12b7c4
   (9) 8d5366123cb560bb606379f90a0bfd4769eecc0557f1b362dcae9012b548b1e5

   Mnemonic: candy maple cake sugar pudding cream honey rich smooth crumble sweet treat

   ⚠️  Important ⚠️  : This mnemonic was created for you by Truffle. It is not secure.
   Ensure you do not use it on production blockchains, or else you risk losing funds.

   truffle(development)>
   ```

   这显示了与区块链进行交互时可以使用的十个账户(和他们的私钥)。

1. 在 Truffle 命令提示符上, 可以通过省略`truffle`前缀来运行 Truffle 命令.
   例如在提示符下运行 `truffle compile` , 键入 `compile`.
   将已编译合约部署到区块链的命令是 `truffle migrate`, 所以在提示符下，键入:

   ```shell
   migrate
   ```

   您将看到以下输出:

   ```sh
   Starting migrations...
   ======================
   > Network name:    'develop'
   > Network id:      4447
   > Block gas limit: 6721975

   1_initial_migration.js
   ======================

      Deploying 'Migrations'
      ----------------------
      > transaction hash:    0x3fd222279dad48583a3320decd0a2d12e82e728ba9a0f19bdaaff98c72a030a2
      > Blocks: 0            Seconds: 0
      > contract address:    0xa0AdaB6E829C818d50c75F17CFCc2e15bfd55a63
      > account:             0x627306090abab3a6e1400e9345bc60c78a8bef57
      > balance:             99.99445076
      > gas used:            277462
      > gas price:           20 gwei
      > value sent:          0 ETH
      > total cost:          0.00554924 ETH

      > Saving migration to chain.
      > Saving artifacts
      -------------------------------------
      > Total cost:          0.00554924 ETH

   2_deploy_contracts.js
   =====================

      Deploying 'ConvertLib'
      ----------------------
      > transaction hash:    0x97e8168f1c05fc40dd8ffc529b9a2bf45cc7c55b07b6b9a5a22173235ee247b6
      > Blocks: 0            Seconds: 0
      > contract address:    0xfb39FeaeF3ac3fd46e2123768e559BCe6bD638d6
      > account:             0x627306090abab3a6e1400e9345bc60c78a8bef57
      > balance:             99.9914458
      > gas used:            108240
      > gas price:           20 gwei
      > value sent:          0 ETH
      > total cost:          0.0021648 ETH

      Linking
      -------
      * Contract: MetaCoin <--> Library: ConvertLib (at address: 0xfb39FeaeF3ac3fd46e2123768e559BCe6bD638d6)

      Deploying 'MetaCoin'
      --------------------
      > transaction hash:    0xee4994097c10e7314cc83adf899d67f51f22e08b920e95b6d3f75c5eb498bde4
      > Blocks: 0            Seconds: 0
      > contract address:    0x6891Ac4E2EF3dA9bc88C96fEDbC9eA4d6D88F768
      > account:             0x627306090abab3a6e1400e9345bc60c78a8bef57
      > balance:             99.98449716
      > gas used:            347432
      > gas price:           20 gwei
      > value sent:          0 ETH
      > total cost:          0.00694864 ETH

      > Saving migration to chain.
      > Saving artifacts
      -------------------------------------
      > Total cost:          0.00911344 ETH

   Summary
   =======
   > Total deployments:   3
   > Final cost:          0.01466268 ETH
   ```

   这显示了已部署合约的交易 ID 和地址。它还包括成本汇总和实时状态更新。

   > 注意: 您的交易哈希，合约地址和帐户将与上述不同。

> 注意: 要查看如何与合约进行互动，请跳至下一部分。

## 备选方案：使用 Ganache 进行迁移

尽管 Truffle Develop 是一个多合一的私有区块链和控制台，但您也可以使用桌面应用程序[Ganache](/ganache)来启动您的私有区块链。
对于那些以太坊和区块链新手来说，Ganache 可能是一个更易于理解的工具，因为它可以预先显示更多信息。

除了运行 Ganache 之外，唯一的额外步骤是它需要编辑 Truffle 配置文件以指向 Ganache 实例。

1. 下载并安装[Ganache](/ganache).

2. 在文本编辑器中打开`truffle-config.js`。 将内容替换为以下内容:

   ```javascript
   module.exports = {
     networks: {
       development: {
         host: "127.0.0.1",
         port: 7545,
         network_id: "*",
       },
     },
   };
   ```

   这将允许使用 Ganache 的默认连接参数进行连接。

3. 保存并关闭该文件。

4. 启动 Ganache。

   ![Ganache](/img/docs/ganache/quickstart/accounts.png)

   _Ganache_

5. 在终端上，将合约迁移到由 Ganache 创建的区块链：

   ```shell
   truffle migrate
   ```

   您将看到以下输出:

   ```sh
   Compiling your contracts...
   ===========================
   > Compiling ./contracts/ConvertLib.sol
   > Compiling ./contracts/MetaCoin.sol
   > Compiling ./contracts/Migrations.sol
   > Artifacts written to /home/david/work/MetaCoin/build/contracts
   > Compiled successfully using:
      - solc: 0.5.16+commit.9c3226ce.Emscripten.clang

   Starting migrations...
   ======================
   > Network name:    'development'
   > Network id:      5777
   > Block gas limit: 6721975 (0x6691b7)

   1_initial_migration.js
   ======================

      Deploying 'Migrations'
      ----------------------
      > transaction hash:    0x3eef05e35ce694c0b7112cc22ba462b9cc0563abc2cc444ee9683b6d89865e3c
      > Blocks: 0            Seconds: 0
      > contract address:    0x8CdaF0CD259887258Bc13a92C0a6dA92698644C0
      > block number:        1
      > block timestamp:     1587421933
      > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
      > balance:             99.9967165
      > gas used:            164175 (0x2814f)
      > gas price:           20 gwei
      > value sent:          0 ETH
      > total cost:          0.0032835 ETH

      > Saving migration to chain.
      > Saving artifacts
      -------------------------------------
      > Total cost:           0.0032835 ETH

   2_deploy_contracts.js
   =====================

      Deploying 'ConvertLib'
      ----------------------
      > transaction hash:    0x23de020bafa41e30615b1d775d2fa9604e876415408e012d1f0faf79eed3a32f
      > Blocks: 0            Seconds: 0
      > contract address:    0x345cA3e014Aaf5dcA488057592ee47305D9B3e10
      > block number:        3
      > block timestamp:     1587421933
      > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
      > balance:             99.99396028
      > gas used:            95470 (0x174ee)
      > gas price:           20 gwei
      > value sent:          0 ETH
      > total cost:          0.0019094 ETH

      Linking
      -------
      * Contract: MetaCoin <--> Library: ConvertLib (at address: 0x345cA3e014Aaf5dcA488057592ee47305D9B3e10)

      Deploying 'MetaCoin'
      --------------------
      > transaction hash:    0x0cc20353422c4d435f72e8e7850f8178f43bf8d00c8c0d09cc8e0ccdfa81b799
      > Blocks: 0            Seconds: 0
      > contract address:    0xf25186B5081Ff5cE73482AD761DB0eB0d25abfBF
      > block number:        4
      > block timestamp:     1587421934
      > account:             0x627306090abaB3A6e1400e9345bC60c78a8BEf57
      > balance:             99.98822922
      > gas used:            286553 (0x45f59)
      > gas price:           20 gwei
      > value sent:          0 ETH
      > total cost:          0.00573106 ETH

      > Saving migration to chain.
      > Saving artifacts
      -------------------------------------
      > Total cost:          0.00764046 ETH

   Summary
   =======
   > Total deployments:   3
   > Final cost:          0.01092396 ETH
   ```

   这显示了已部署合约的交易 ID 和地址。它还包括成本汇总和实时状态更新。

   > 注意: 您的交易 ID 和合约地址可能与上述不同。

6. 在 Ganache 中，单击`Transactions`按钮以查看已处理事务。

7. 要与合约进行交互，可以使用 Truffle 控制台。Truffle 控制台类似于 Truffle Develop，不同之处在于它连接到现有的区块链（在本例中为 Ganache 生成的区块链）。

   ```shell
   truffle console
   ```

   您将看到以下提示:

   ```sh
   truffle(development)>
   ```

## 与合约互动

以下列方式使用控制台与合约互动:

> 注意: 在这些示例中，我们使用的是`web3.eth.getAccounts()`， 它返回一个 promise，该 promise 解析为助记符生成的所有帐户的数组。
> 因此，鉴于上述助记符生成的地址，指定 `(await web3.eth.getAccounts())[0]` 等同于地址 `0x627306090abab3a6e1400e9345bc60c78a8bef57`.

从 Truffle v5 开始，该控制台支持异步/等待功能，从而使与合约的交互更加简单。

- 首先建立部署的 MetaCoin 合约实例和 Truffle 的内置区块链或 Ganache 创建的帐户:

  ```javascript
  truffle(development)> let instance = await MetaCoin.deployed()
  truffle(development)> let accounts = await web3.eth.getAccounts()
  ```

- 检查已部署合约的帐户的元币余额:

  ```javascript
  truffle(development)> let balance = await instance.getBalance(accounts[0])
  truffle(development)> balance.toNumber()
  ```

- 查看该余额有多少以太币价值（并注意该合约将一个元币定义为价值 2 以太币）:

  ```javascript
  truffle(development)> let ether = await instance.getBalanceInEth(accounts[0])
  truffle(development)> ether.toNumber()
  ```

- 将一些元币从一个帐户转移到另一个帐户:

  ```javascript
  truffle(development) > instance.sendCoin(accounts[1], 500);
  ```

- 检查*接收*元币的账户余额：

  ```javascript
  truffle(development)> let received = await instance.getBalance(accounts[1])
  truffle(development)> received.toNumber()
  ```

- 检查*发送*元币的账户余额:

  ```javascript
  truffle(development)> let newBalance = await instance.getBalance(accounts[0])
  truffle(development)> newBalance.toNumber()
  ```

## 继续学习

本快速入门向您展示了 Truffle 项目生命周期的基础知识, 但有更多的要学习. 请继续阅读我们的[文档](/docs)的其余部分，尤其是我们的[教程](/tutorials)，以了解更多信息。
