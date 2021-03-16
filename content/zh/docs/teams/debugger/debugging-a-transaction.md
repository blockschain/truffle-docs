---
title: 调试交易
weight: 1
---

注意: Truffle 团队目前仅允许您在[Ganache 沙箱](/docs/teams/sandboxes/sandboxes-overview)上调试事务.
即将提供对公共网络（例如<code>Görli</code> testnet 或<code> mainnet </code>）的支持。

可从 **<span class="inline-menu-item"><i class="fal fa-parachute-box"></i>DEPLOYMENTS</span>** 页面访问调试器。
从这里，[选择部署](/docs/teams/deployments/deployment-details)，其中包括接收您要调试的事务的合约。
在下面的示例屏幕截图中，这是`deployment-01`。

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-100" src="/img/docs/teams/debugger-deployments.png" alt="Teams Deployments">
  <figcaption class="text-center"> Truffle 团队部署屏幕。</figcaption>
</figure>

在此屏幕上，您可以单击合约右侧的 **<span class="inline-button"><i class="fas fa-heart-rate"></i> MONITOR</span>** 以查看仅发送到该合约地址的交易, 或 **TRANSACTIONS** 标签以查看与整个部署相关的所有交易.

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-100" src="/img/docs/teams/debugger-deployment.png" alt="Teams Deployment">
  <figcaption class="text-center"> Truffle 团队部署屏幕。</figcaption>
</figure>

假设您的合约已收到一项或多项交易，您现在将看到类似于以下屏幕截图的列表。

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-100" src="/img/docs/teams/debugger-monitoring-transactions.png" alt="Teams Transaction Monitoring">
  <figcaption class="text-center">The Truffle Teams Transaction Monitoring screen.</figcaption>
</figure>

注意: The Truffle Teams Debugger is currently only available for transactions excuted sent to contracts in [Ganache sandboxes](/docs/teams/sandboxes/sandboxes-overview) and accordingly the DEBUG button will show as disabled for other networks.
Debugging transactions made against public networks will be available in a forthcoming release.

注意: The Truffle Teams Debugger is currently available as part of our <code>Early Access</code> program and, as such, the <span class="inline-button"><i class="fas fa-debug"></i> DEBUG</span> button will not be visible until it's enabled.
It requires opting-in, as it gives you access to cutting-edge and potentially unstable features, which can be done by clicking Settings > Advanced.

可以通过单击给定事务右侧的 **<span class="inline-button"><i class="fas fa-debug"></i> DEBUG</span>** 按钮来启动调试器。
