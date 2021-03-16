---
title: 使用调试器
weight: 2
---

在本节中，我们将探讨调试器用户界面的各个元素以及实际调试事务时涉及的步骤。
让我们探索一个 Truffle Teams 调试器接口的示例，其中正在调试一个简单的 ERC721 令牌实现。

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-100" src="/img/docs/teams/debugger-transaction-01.png" alt="Teams Debugger Interface">
  <figcaption class="text-center"> Truffle 团队调试器界面。</figcaption>
</figure>

首先要注意的是页面标题中的事务哈希(`0x82f668a...`)。
标题包括交易是否最终成功<i class="fas fa-check-circle" style="color: #00A311"></i> 或失败 <i class="fas fa-times-circle" style="color: #D60000"></i>的直观表示 .

这是一个有用的参考，因为它使您可以抢先知道执行完成后是否期望状态消息.

有关更多信息，请参见[状态消息](/docs/teams/debugger/using-the-debugger#status-messages)部分。

## 调试器控制面板

在调试器界面中，您将找到调试器的控制面板。

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-50" src="/img/docs/teams/debugger-control-palette.png" alt="Teams Debugger Control Palette">
  <figcaption class="text-center"> Truffle 团队调试器控制面板。</figcaption>
</figure>

从左到右，控件及其相关操作的说明如下。请注意，您也可以将控件悬停以显示其关联名称。
请注意，方括号包含每个命令的相应键盘快捷键。

- <code>Continue</code> - 继续直到到达下一个断点或执行最后一行 ("c" or "F8")
- <code>Step Over</code> - 跨过当前行 ("o" or "F10")
- <code>Step Into</code> - 进入当前正在评估的函数调用或合约创建 ("i" or "F11")
- <code>Step Out</code> - 退出当前正在运行的功能 ("u" or "Shift+F11")
- <code>Restart</code> - 重新启动调试器会话 ("r")

## 源文件

将作为带有事务文件执行路径的一部分访问的源文件将由带有合约文件名的选项卡表示。
值得注意的是，您的项目可能包含的文件数量超过此处显示的文件数量。

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-50" src="/img/docs/teams/debugger-interface-tabs.png" alt="Teams Debugger Source File Tabs">
  <figcaption class="text-center">Truffle Teams调试器的“源文件”选项卡。</figcaption>
</figure>

调试器选项卡有两个值得注意的视觉提示。
第一个是“打开的标签页”，这意味着您正在查看下面的文件代码，并用浅绿色背景表示。
第二个是“活动选项卡”，它由橙色圆圈<i class="fas fa-dot-circle" style="color: #dc9e5b"></i>表示，表示调试器当前在该文件中暂停。

当您使用调试器的控件逐步完成事务时，您可能会看到活动的选项卡更新。
请注意，当代码进入后，打开的标签也会更新。

## 调试器源视口

As the core of the Truffle Teams Debugger is the source viewport.
This is a read-only display of the code that the transaction will be stepping through as part of its execution.

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-50" src="/img/docs/teams/debugger-source-viewport.png" alt="Teams Debugger Source Viewport">
  <figcaption class="text-center">The Truffle Teams Debugger Source Viewport.</figcaption>
</figure>

The main thing to note is the active line which is highlighted in yellow.
As your step through your transaction this will update accordingly.

## 调试器变量检查器

The variable inspector shows the variable values for the current transaction execution context, including contract state, local function, and global variables.
The inspector uses a tree-like explorer enabling you to drill down by clicking on a given branch, represented by the green right-facing caret icon <i class="fas fa-caret-right" style="color: #17B89D"></i>.

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-50" src="/img/docs/teams/debugger-variables.png" alt="Teams Debugger Variable Inspector">
  <figcaption class="text-center">The Truffle Teams Debugger Variable Inspector.</figcaption>
</figure>

## 断点

Located in the lower right corner of the screen is the breakpoint tray.
Breakpoints are added to the tray by clicking on a given line number or just to the left in the line's "gutter".
They can subsequently be removed by clicking in the same location or on the circular cross <i class="fas fa-times-circle" style="color: #BCA296"></i> to the right of the breakpoint entry in the tray itself.

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-100" src="/img/docs/teams/debugger-breakpoints.png" alt="Teams Debugger Breakpoints">
  <figcaption class="text-center">The Truffle Teams Debugger Breakpoints.</figcaption>
</figure>

Functionally, breakpoints will cause code execution to stop (or break) upon being reached.
At this point it's common to inspect state via the [Variable Inspector](#debugger-variable-inspector) or continue [stepping through](#debugger-control-palette) to ensure your code is behaving as expected or when tracking down a bug.

Lastly, note that clicking on a given breakpoint within the tray will jump you to the corresponding tab and line.
This is particularly useful when navigating more complex contracts that comprise of multiple files.

## 状态讯息

If your transaction's execution ultimately fails, a banner appear after the `REVERT` happens.
An associated status message or reason string will be shown if one exists.

<figure class="screenshot">
  <img class="figure-shadow mb-2 w-100" src="/img/docs/teams/debugger-status-message.png" alt="Teams Debugger Status Message">
  <figcaption class="text-center">The Truffle Teams Debugger Status Message.</figcaption>
</figure>

As shown in the example, the transaction failed with the `ERC721: token already minted` reason string.
