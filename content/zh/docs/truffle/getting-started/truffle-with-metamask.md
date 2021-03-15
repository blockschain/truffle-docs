---
title: Truffle 和 MetaMask
weight: 6
---

在您可以在浏览器中与智能合同互动之前, 确保编译，部署， 并且您正在通过`web3`在客户端JavaScript中与他们交流. 
我们建议使用 [@truffle/contract](https://github.com/trufflesuite/truffle/tree/master/packages/contract) 图书馆,因为它使互动与合同更容易，更强大.

<p class="alert alert-info">
<strong>Note</strong>: 有关这些主题的更多信息，包括使用 `@truffle/contract`, 看看我们的 <a href="/tutorials/pet-shop">Pet Shop</a> 或者 <a href="/tutorials/robust-smart-contracts-with-openzeppelin">TutorialToken</a> 教程.
</p>

一旦完成上述情况，您就可以使用MetAMask.

## 什么是MetaMask？

[MetaMask](https://metamask.io/) 是在浏览器中与DAPP交互的最简单方法. 
它是Chrome或Firefox的扩展，它连接到Etereum网络而不在浏览器机器上运行完整节点. 
它可以连接到主要的Ethereum网络，任何测试网络（Ropsten，Kovan和Rinkeby）, 或本地区块链，例如由[ganache](/ganache)或Truffle Develop创建的区块链条.

![MetaMask](/img/docs/truffle/truffle-with-metamask/metamask.png)

有关块块的开发，这意味着我们可以同样地使用我们的DAPP，用户将在现场网络上与之交互。

## 安装MetaMask

* 为Chrome安装MetAmask, 转到[Chrome Web Store](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn) 然后点击这一点 **Add to Chrome** 按钮.

* 为Firefox安装MetAmask, 转到[Firefox附加页面](https://addons.mozilla.org/en-US/firefox/addon/ether-metamask/) 然后点击这一点 **Add to Firefox** 按钮.

我们的前端准备好使用和安装了Metamask，我们已准备好在所有荣耀中看到我们的DAPP。

## 将MetaMask与Ganache一起使用

[Ganache](/ganache) 是一个图形应用程序，它运行一个可以用于测试目的的区块链. 它运行 `127.0.0.1:7545`.

<p class="alert alert-info">
<strong>Note</strong>: 我们建议指定 `127.0.0.1` 代替 `localhost` 因为地址不需要网络连接，因此更适合开发.
</p>

### 检测MetaMask的web3注入

在潜水之前，我们需要确保DAPP检查MetAmask的`web3`实例并且扩展本身与Ganache正确配置.

metamask注入自己的`web3`实例, 所以我们想确保我们检查一下. 窗口加载后执行以下检查:

```javascript
// Is there is an injected web3 instance?
if (typeof web3 !== 'undefined') {
  App.web3Provider = web3.currentProvider;
  web3 = new Web3(web3.currentProvider);
} else {
  // If no injected web3 instance is detected, fallback to Ganache.
  App.web3Provider = new web3.providers.HttpProvider('http://127.0.0.1:7545');
  web3 = new Web3(App.web3Provider);
}
```

### 设置Metamask.

要使用MetAmask使用GaNache，请单击浏览器中的MetAmask图标，此屏幕将出现:

![MetaMask initial screen](/img/docs/truffle/truffle-with-metamask/metamask-create-password.png)

*MetAmask初始屏幕*

点击 **Import with seed phrase**. 在标记的盒子里 **Wallet Seed**, 输入启动Ganache时显示的助记符.

<p class="alert alert-danger">
<strong>警告</strong>: 请勿在主Ethereum网络（MainNet）上使用此助记符. 确保将网络设置为"Private Network" (使用 "Custom RPC" 环境). 有关详细信息，请参阅下文.
</p>

在下面输入密码，然后单击 **OK**.

![MetaMask seed phrase](/img/docs/truffle/truffle-with-metamask/metamask-seed-phrase.png)

*MetaMask seed phrase*

现在我们需要将MetAmask连接到Ganache创建的区块链. 单击显示的菜单 "Main Network" 并选择 **Custom RPC**.

![MetaMask network menu](/img/docs/truffle/truffle-with-metamask/metamask-select-network.png)

*MetaMask network menu*

在标题的框中 "New RPC URL" (在 - 的右边 "New Network") 进入 `http://127.0.0.1:7545` 然后点击 **Save**.

<!--Add image from pet shop tutorial when updated for Ganache -->

顶部的网络名称将切换到说明 "Private Network". 单击当前窗口的右上角的十字架关闭页面并返回“帐户”页面。

现在我们将MetAmask连接到Ganache，您将被带到帐户屏幕。 
Ganache创建的每个帐户都有100个以太网。 
第一个账户应该少于其他账户，因为该帐户为智能合同部署提供了气体。 
由于您已将智能合同部署到网络，此帐户已支付.

单击右上角的“帐户”图标以创建新帐户，其中前10个将对应于启动Ganache时显示的10个帐户。

![MetaMask account](/img/docs/truffle/truffle-with-metamask/metamask-account1.png)

*MetaMask account*

## 结合使用MetaMask和Truffle Develop

Truffle Develop是一个命令行应用程序，运行临时区块链接，也用于测试目的。 
它运行`127.0.0.1:9545`.

<p class="alert alert-info">
<strong>Note</strong>: 我们建议指定 `127.0.0.1` 代替 `localhost` 因为地址不需要网络连接，因此更适合开发.
</p>

使用带有松露的元掩模开发非常类似于Ganache的MetAmask。 
唯一的区别在于默认情况下，Truffle开发运行 `127.0.0.1:9545`, 所以你要编辑上面的web3代码说:

  ```javascript
  // Is there is an injected web3 instance?
  if (typeof web3 !== 'undefined') {
    App.web3Provider = web3.currentProvider;
    web3 = new Web3(web3.currentProvider);
  } else {
    // If no injected web3 instance is detected, fallback to Truffle Develop.
    App.web3Provider = new web3.providers.HttpProvider('http://127.0.0.1:9545');
    web3 = new Web3(App.web3Provider);
  }
  ```

在Metamask中，进入时 "New RPC URL", 输入 `http://127.0.0.1:9545`.

## 将MetaMask与Ganache CLI一起使用

使用带有Ganache CLI的元掩码也与Ganache非常类似. 
唯一的区别是Ganache CLI默认情况下运行 `http://127.0.0.1:8545` 所以你要编辑上面的web3代码说:

  ```javascript
  // Is there is an injected web3 instance?
  if (typeof web3 !== 'undefined') {
    App.web3Provider = web3.currentProvider;
    web3 = new Web3(web3.currentProvider);
  } else {
    // If no injected web3 instance is detected, fallback to Ganache CLI.
    App.web3Provider = new web3.providers.HttpProvider('http://127.0.0.1:8545');
    web3 = new Web3(App.web3Provider);
  }
  ```

在Metamask中，进入时 "New RPC URL", 输入 `http://127.0.0.1:8545`.
