---
title: Truffle 和 MetaMask
weight: 6
---

在您可以在浏览器中与智能合约互动之前, 确保编译，部署， 并且您正在通过`web3`在客户端 JavaScript 中与他们交流.
我们建议使用 [@truffle/contract](https://github.com/trufflesuite/truffle/tree/master/packages/contract) 图书馆,因为它使互动与合约更容易，更强大.

注意: 有关这些主题的更多信息，包括使用 `@truffle/contract`, 看看我们的 [TutorialToken](/tutorials/pet-shop">Pet Shop</a> 或者 <a href="/tutorials/robust-smart-contracts-with-openzeppelin) 教程.

一旦完成上述情况，您就可以使用 MetAMask.

## 什么是 MetaMask？

[MetaMask](https://metamask.io/) 是在浏览器中与 DAPP 交互的最简单方法.
它是 Chrome 或 Firefox 的扩展，它连接到 Etereum 网络而不在浏览器机器上运行完整节点.
它可以连接到主要的 Ethereum 网络，任何测试网络（Ropsten，Kovan 和 Rinkeby）, 或本地区块链，例如由[ganache](/ganache)或 Truffle Develop 创建的区块链条.

![MetaMask](/img/docs/truffle/truffle-with-metamask/metamask.png)

有关块块的开发，这意味着我们可以同样地使用我们的 DAPP，用户将在现场网络上与之交互。

## 安装 MetaMask

- 为 Chrome 安装 MetAmask, 转到[Chrome Web Store](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn) 然后点击这一点 **Add to Chrome** 按钮.

- 为 Firefox 安装 MetAmask, 转到[Firefox 附加页面](https://addons.mozilla.org/en-US/firefox/addon/ether-metamask/) 然后点击这一点 **Add to Firefox** 按钮.

我们的前端准备好使用和安装了 Metamask，我们已准备好在所有荣耀中看到我们的 DAPP。

## 将 MetaMask 与 Ganache 一起使用

[Ganache](/ganache) 是一个图形应用程序，它运行一个可以用于测试目的的区块链. 它运行 `127.0.0.1:7545`.

注意: 我们建议指定 `127.0.0.1` 代替 `localhost` 因为地址不需要网络连接，因此更适合开发.

### 检测 MetaMask 的 web3 注入

在潜水之前，我们需要确保 DAPP 检查 MetAmask 的`web3`实例并且扩展本身与 Ganache 正确配置.

metamask 注入自己的`web3`实例, 所以我们想确保我们检查一下. 窗口加载后执行以下检查:

```javascript
// Is there is an injected web3 instance?
if (typeof web3 !== "undefined") {
  App.web3Provider = web3.currentProvider;
  web3 = new Web3(web3.currentProvider);
} else {
  // If no injected web3 instance is detected, fallback to Ganache.
  App.web3Provider = new web3.providers.HttpProvider("http://127.0.0.1:7545");
  web3 = new Web3(App.web3Provider);
}
```

### 设置 Metamask.

要使用 MetAmask 使用 GaNache，请单击浏览器中的 MetAmask 图标，此屏幕将出现:

![MetaMask initial screen](/img/docs/truffle/truffle-with-metamask/metamask-create-password.png)

_MetAmask 初始屏幕_

点击 **Import with seed phrase**. 在标记的盒子里 **Wallet Seed**, 输入启动 Ganache 时显示的助记符.

<p class="alert alert-danger">
警告: 请勿在主Ethereum网络（MainNet）上使用此助记符. 确保将网络设置为"Private Network" (使用 "Custom RPC" 环境). 有关详细信息，请参阅下文.

在下面输入密码，然后单击 **OK**.

![MetaMask seed phrase](/img/docs/truffle/truffle-with-metamask/metamask-seed-phrase.png)

_MetaMask seed phrase_

现在我们需要将 MetAmask 连接到 Ganache 创建的区块链. 单击显示的菜单 "Main Network" 并选择 **Custom RPC**.

![MetaMask network menu](/img/docs/truffle/truffle-with-metamask/metamask-select-network.png)

_MetaMask network menu_

在标题的框中 "New RPC URL" (在 - 的右边 "New Network") 进入 `http://127.0.0.1:7545` 然后点击 **Save**.

<!--Add image from pet shop tutorial when updated for Ganache -->

顶部的网络名称将切换到说明 "Private Network". 单击当前窗口的右上角的十字架关闭页面并返回“帐户”页面。

现在我们将 MetAmask 连接到 Ganache，您将被带到帐户屏幕。
Ganache 创建的每个帐户都有 100 个以太网。
第一个账户应该少于其他账户，因为该帐户为智能合约部署提供了气体。
由于您已将智能合约部署到网络，此帐户已支付.

单击右上角的“帐户”图标以创建新帐户，其中前 10 个将对应于启动 Ganache 时显示的 10 个帐户。

![MetaMask account](/img/docs/truffle/truffle-with-metamask/metamask-account1.png)

_MetaMask account_

## 结合使用 MetaMask 和 Truffle Develop

Truffle Develop 是一个命令行应用程序，运行临时区块链接，也用于测试目的。
它运行`127.0.0.1:9545`.

注意: 我们建议指定 `127.0.0.1` 代替 `localhost` 因为地址不需要网络连接，因此更适合开发.

使用带有 Truffle 的元掩模开发非常类似于 Ganache 的 MetAmask。
唯一的区别在于默认情况下，Truffle 开发运行 `127.0.0.1:9545`, 所以你要编辑上面的 web3 代码说:

```javascript
// Is there is an injected web3 instance?
if (typeof web3 !== "undefined") {
  App.web3Provider = web3.currentProvider;
  web3 = new Web3(web3.currentProvider);
} else {
  // If no injected web3 instance is detected, fallback to Truffle Develop.
  App.web3Provider = new web3.providers.HttpProvider("http://127.0.0.1:9545");
  web3 = new Web3(App.web3Provider);
}
```

在 Metamask 中，进入时 "New RPC URL", 输入 `http://127.0.0.1:9545`.

## 将 MetaMask 与 Ganache CLI 一起使用

使用带有 Ganache CLI 的元掩码也与 Ganache 非常类似.
唯一的区别是 Ganache CLI 默认情况下运行 `http://127.0.0.1:8545` 所以你要编辑上面的 web3 代码说:

```javascript
// Is there is an injected web3 instance?
if (typeof web3 !== "undefined") {
  App.web3Provider = web3.currentProvider;
  web3 = new Web3(web3.currentProvider);
} else {
  // If no injected web3 instance is detected, fallback to Ganache CLI.
  App.web3Provider = new web3.providers.HttpProvider("http://127.0.0.1:8545");
  web3 = new Web3(App.web3Provider);
}
```

在 Metamask 中，进入时 "New RPC URL", 输入 `http://127.0.0.1:8545`.
