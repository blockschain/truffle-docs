---
title: 添加存储库
weight: 2
---

您第一次登录 Truffle 团队时，Github 将提示您在一个或多个存储库上安装它。
在某些情况下，您可能希望在初始安装后添加存储库。
例如，如果它在注册 Truffle 团队后创建。

将存储库添加到松露团队, 导航[https://my.truffleteams.com](https://my.truffleteams.com).
点击 `LOGIN WITH GITHUB` 一旦您成功登录，您将被重定向到 Truffle Teams 主页.
登录后，您还可以单击任何页面右上角的`Truffle Teams`徽标被重定向到主页。
从那里，您可以滚动到页面的底部，然后单击 <span class="inline-button">ADD REPOSITORY</span>, 这将带你到 Truffle Teams GitHub 应用程序页面 您可以在其中选择要添加到团队的存储库.

<figure>
  <img class="figure-shadow mb-2" src="/img/docs/teams/add-repo-00.png" alt="Deployment Selection Screen" style="width: 100%">
  <figcaption class="text-center font-italic">具有和没有存储库的回购选择（主页）屏幕。</figcaption>
</figure>

点击 `Configure`继续配置松露团队.

![Truffle Teams DATA view](/img/docs/teams/add-repo-01.png)

接下来将是具有`Configure >`链接上已安装的团队的存储库列表。
单击其中一个存储库中的一个，没有该链接将 Truffle 团队安装到该存储库上。

<p class="alert alert-info">
<strong>Note</strong>: 此时，您可能会提示您的GitHub密码。
</p>

![Truffle团队数据视图](/img/docs/teams/add-repo-02.png)

您将到达 Truffle Teams 的设置页面。
靠近底部的纸张 `Repository access`.
选择任一个 `All repositories` 将此帐户中的所有存储库添加到团队中或者 `Only select repositories` 从下拉列表中选择单个存储库.

![Truffle Teams DATA view](/img/docs/teams/add-repo-03.png)

选择一个或多个存储库后，单击绿色`Save` 按钮。
您将被重定向到此所有者的 Truffle 团队设置页面的顶部，并使用确认消息。

您现在可以返回 Truffle 团队，以查看您的新添加的存储库！

<p class="alert alert-info">
<strong>Note</strong>: Truffle团队只会构建存储库根root的存储库。 
它在构建之前查找根目录中的<code>truffle-config.js</code> 或者 <code>truffle.js</code>配置。 
在[配置文档](/docs/teams/reference/configuration#repository-structure)中阅读更多信息.
</p>
