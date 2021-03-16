---
title: "用Truffle Teams新的调试器轻快地和上下调试"
date: "2020-11-12"
author: "Josh Quintal"
published: true
excerpt: "如果您使用过Truffle的调试器，则会知道这是一流的。 直到现计，它已被限制在命令行。 今天，调试器会在 Truffle 团队中的一个GUI中脱离控制台！"
image: "/img/blog/debug-quickly-and-in-context-with-truffle-teams-new-debugger/blog-thumbnail.png"
---

![Truffle Teams Debugger Banner](/img/blog/debug-quickly-and-in-context-with-truffle-teams-new-debugger/blog-header.png)

如果您使用过 Truffle 的调试器，则会知道这是一流的。直到现计，它已被限制在命令行。今天，调试器会在 Truffle 团队中的一个 GUI 中脱离控制台！这是一个巨大的工作流程增强 - 允许我们在我们已经查看的地方调试交易 - 通过部署详细信息屏幕或监视各个合约。让我们来看看！

<i class="fas fa-info-circle"></i> 注意: To use the debugger right away, you'll need to opt-in to [Truffle Teams Early Access](/blog/try-new-features-first-with-truffle-teams-early-access).

## 启动调试器

To launch the debugger, we just need to find a transaction. Head over to the Deployments screen and select a deployment. From there select the transactions tab or click the monitoring button for a contract. You'll notice there's a debug button on each transaction card; clicking it will open the Truffle Teams debugger.

</div></div></div>

<figure class="breakout">
  <img class="mb-4 w-100 w-md-70 figure-shadow" src="/img/blog/debug-quickly-and-in-context-with-truffle-teams-new-debugger/teams-debugger-1.png" alt="All transaction cards now have a debug button">
  <figcaption class="text-center font-italic">Debugging is only a click away!</figcaption>
</figure>

<div class="container container-post"><div class="row justify-content-center"><div class="col">

## 导航 UI.

Starting at the top, you'll see the transaction hash along with an icon noting its status and, if applicable, the accompanying error message (1). Below that we have our functions, from left to right: Step Next, Step Over, Step In, Step Out, and Reset (2). Next we have some tabs showing the contracts included in this transaction (3). Finally we have two panes, one showing our Solidity with the current step highlighted in yellow (4). The second with our variables (5).

</div></div></div>

<figure class="breakout">
  <img class="mb-4 w-100 figure-shadow" src="/img/blog/debug-quickly-and-in-context-with-truffle-teams-new-debugger/teams-debugger-2.png" alt="The debugger in action on a failed transaction">
  <figcaption class="text-center font-italic">Debugging a failed transaction.</figcaption>
</figure>

<div class="container container-post"><div class="row justify-content-center"><div class="col">

At the moment some other enhancements, including breakpoints and syntax highlighting, are coming soon. We wanted to get this powerful feature in your hands as quickly as possible, so we're releasing it now via Early Access. For more information on what to expect from early access, check out [the Truffle Teams Early Access blog post](/blog/try-new-features-first-with-truffle-teams-early-access).

For more information, check out [the Truffle Teams Debugger docs](/docs/teams/debugger/debugging-a-transaction) or for general information about Truffle's debugger, check out [the Truffle Debugger docs](/docs/truffle/getting-started/debugging-your-contracts).

<div class="mt-12 text-center">
  <a class="btn btn-truffle mt-3" href="https://my.truffleteams.com/" target="_blank">CHECK OUT THE TRUFFLE TEAMS DEBUGGER</a>
</div>

## 继续谈话

We want Truffle Teams to be the most effective DevOps tool in the blockchain space for both new and existing teams. Let us know what you think about the new deployment views, or if your team has other needs we haven't met yet.

Continue the conversation with your fellow Trufflers in our Slack community!

<div class="mt-12 text-center">
  <a class="btn btn-truffle mt-3" href="https://join.slack.com/t/truffle-community/shared_invite/zt-8wab0bnl-KcugRAqsY9yeNJYcnanfLA" target="_blank">SIGN UP FOR THE TRUFFLER SLACK</a>
</div>

Thanks!

_Josh Quintal, Head of Product & Marketing_
