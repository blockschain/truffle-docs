---
title: 调试您的合约
weight: 9
---

Truffle 包含一个集成的调试器，以便您可以调试与您的合约进行的交易。
此调试器外观和感觉像现有的命令行调试器可用于传统开发环境。

## 概述

<p class="alert alert-info m-t-2">

Truffle v5.1 更新: `truffle test --debug`.

使用新的全局`debug()`设置 JavaScript 测试中的断点！
[See below](#in-test-debugging).

<p class="alert alert-info m-t-2">

Truffle v5.1.29 更新: `truffle debug --fetch-external`.

调试交易，涉及在[Sourcify](https://etherscan.io/">etherscan</a>上核实的项目中的合约! (并且 v5.1.32, 它也适用 <a href="https://github.com/ethereum/sourcify) !)
[See below](#debugging-external-contracts-with-verified-source).

在区块链上调试事务与调试传统应用程序不同 (例如，用 C ++或 JavaScript 编写的应用程序).
在块链中调试事务时，您无法实时运行代码;相反，您正在踩到该事务的历史执行，并将其映射到其关联的代码上。
这使我们在调试中提供了许多自由，因为我们可以随时调试任何事务，只要我们拥有交易与交易的合约的代码和工件。
将这些代码和文物视为类似于传统调试器所需的调试符号。

为了调试交易，您需要以下内容:

- Truffle 4.0 或以上。
- 您所希望的区块链上的交易的哈希。 (如果您使用内置区块链并尝试调试测试执行，则可以通过运行 `truffle develop --log`获取哈希值.)
- 交易遇到的源代码和工件。

请注意，如果您所需的交易导致异常或者它耗尽气体，则可以没关系。
该交易仍然存在于链上，因此您仍然可以调试它！

警告：对启用优化编译的合约调试交易可能无法可靠地工作。

## 在测试调试

Truffle V5.1 及以上提供了 `truffle test --debug` 旗帜 和关联`debug()`全球功能, 允许您中断测试到调试特征。

如下所述，而不是捕获交易哈希, 简单地包装任何合约运作 `debug()`, 像这样:

```javascript
it("should succeed", async function () {
  // wrap what you want to debug with `debug()`:
  await debug(myContract.myFunction(accounts[1], { from: accounts[0] }));
  //           ^^^^^^^^^^^^^^^^^^ wrap contract operation ^^^^^^^^^^^^^^
});
```

Then, run `truffle test --debug`. Truffle will compile your sources and run
your tests as normal until reaching the operation in question. At this point,
Truffle will interrupt the normal test flow and start the debugger, allowing
you to set breakpoints, inspect Solidity variables, etc.

See [Writing tests in JavaScript](/docs/truffle/writing-tests-in-javascript)
for more information on `truffle test`, and see
[Interacting with your contracts](/docs/truffle/getting-started/interacting-with-your-contracts)
to learn about contract operations.

<p class="alert alert-warning">
注意: This feature currently doesn't work with reverted transactions;
until we fix this, you can debug those with direct use of `truffle debug`.

### 调试只读呼叫

Running the debugger from inside your JS tests allow additional functionality
beyond which `truffle debug <txHash>` can provide.

Beyond just debugging transactions, in-test debugging allows you to debug
read-only calls as well.

```javascript
it("should get latest result", async function () {
  // wrap what you want to debug with `debug()`:
  const result = await debug(myContract.getResult("latest"));
  //                          ^^^^^ read-only function ^^^^^
});
```

## 命令

To use the debugger, gather the transaction you'd like to debug then run the following:

```shell
$ truffle debug <transaction hash>
```

Using a transaction starting with `0x8e5dadfb921dd...` as an example, the command would look as follows:

```shell
$ truffle debug 0x8e5dadfb921ddddfa8f53af1f9bd8beeac6838d52d7e0c2fe5085b42a4f3ca76
```

This will launch the debugging interface described below.

If you simply want to open the debugger to get it ready, so that you can debug a transaction later, you can also simply run:

```shell
$ truffle debug
```

Regardless of how you start the debugger, once it is running you are not limited to debugging only the transaction you launched it with; it is possible to unload the current transaction and load a new one, as described below.

You can specify the network you want to debug on with the `--network` option:

```shell
$ truffle debug [<transaction hash>] --network <network>
```

And if you want to debug your [Solidity test contracts](../testing/writing-tests-in-solidity), you can pass the `--compile-tests` option:

```shell
$ truffle debug [<transaction hash>] --compile-tests
```

And with the `--fetch-external` option ([see below](#debugging-external-contracts-with-verified-source)), you can debug contract instances outside your project that have verified source code on [Etherscan](https://etherscan.io/) or [Sourcify](https://github.com/ethereum/sourcify). When using this option, you must specify a transaction hash to debug, and you will not be able to switch transactions from inside the debugger.

```shell
$ truffle debug <transaction hash> --fetch-external --network <network>
```

<p class="alert alert-info m-t-2">

Faster debugger startup:

If your project was not compiled all at once (or under certain other
conditions), the debugger will have to do its own compile of your project on
startup. This can be very slow. If you compile your whole project at once,
however, the debugger can likely avoid the initial recompile, speeding up
startup greatly.

## 使用已验证来源调试外部合约

If you pass the `--fetch-external` option, the debugger will attempt to download verified source code off of [Etherscan](https://etherscan.io/) and [Sourcify](https://github.com/ethereum/sourcify) for any addresses involved in the transaction that it cannot find source code for in your project. You can of course debug such transactions without this option, but when stepping through the transaction the external calls to these unrecognized contracts will simply be skipped over.

This option can also be abbreviated `-x`.

If you have an Etherscan API key, you can include it in your configuration file and the debugger will use it when downloading source from Etherscan. Including this can speed up downloads.

Example:

```javascript
module.exports = {
  /* ... rest of truffle-config.js ... */
  etherscan: {
    apiKey: "0123456789abcdef0123456789abcdef", //replace this with your API key if you have one
  },
};
```

## 调试界面

Starting the debugger will open an interface familiar to those that have debugged other types of applications. When it starts, you'll see the following:

- A list of addresses either transacted against or created during the course of this transaction.
- A list of available commands for using the debugger.
- And the initial entry point for the transaction, including contract source file and code preview.

The `enter` key is set to perform the last command entered. When the debugger starts, the `enter` key is set to step to the next logical source code element encountered during execution (i.e., the next expression or statement evaluated by the Ethereum virtual machine). At this point you can press `enter` to step through the transaction, or enter one of the available commands to analyze the transaction in more detail. The list of commands is detailed below.

### (o) step over

This command steps over the current line, relative to the position of the statement or expression currently being evaluated in the Solidity source file. Use this command if you don't want to step into a function call or contract creation on the current line, or if you'd like to quickly jump to a specific point in the source file.

### (i) step into

This command steps into the function call or contract creation currently being evaluated. Use this command to jump into the function and quickly start debugging the code that exists there.

### (u) step out

This command steps out of the currently running function. Use this command to quickly get back to the calling function, or end execution of the transaction if this was the entry point of the transaction.

### (n) step next

This command steps to the next logical statement or expression in the source code. For example, evaluating sub expressions will need to occur first before the virtual machine can evaluate the full expression. Use this command if you'd like to analyze each logical item the virtual machine evaluates.

### (;) step instruction

This command allows you to step through each individual instruction evaluated by the virtual machine. This is useful if you're interested in understanding the low level bytecode created by the Solidity source code. When you use this command, the debugger will also print out the stack data at the time the instruction was evaluated. (If additional data displays have been turned on with the `p` command, those will be shown too.)

You can also use this command with a numerical argument, to step that many times.

### (p) print instruction

This commands prints the current instruction and stack data, but does not step to the next instruction. Use this when you'd like to see the current instruction and stack data after navigating through the transaction with the logical commands described above.

This command can also print locations other than the stack, if you want to view memory, storage, or calldata. Simply type `p memory` to show memory along with the other information, `p storage` for storage, or `p calldata` for calldata. Each of these can also be abbreviated, e.g. `p mem`; they can also be combined, e.g. `p mem sto`.

You can also add these extra locations to the default display with `+`; e.g., `p +mem` will make it so that memory will always be displayed when you enter `p` or `;`, and `p -mem` will turn this off. You can even turn off the stack display with `p -sta`, or force it to display with `p sta`. All of these options can again be combined.

### (g) turn on generated sources

When using Solidity 0.7.2 or later, you can use this option to allow the debugger to step into the internal assembly routines that Solidity generates. You can always advance into these with the `;` command, but this option allows the other debugger commands (`n`, `i`, `o`, `u`) to step into these routines as well.

### (G) turn off generated sources

This command undoes the `g` command, returning the debugger to its default behavior with regard to generated sources.

Note that when generated sources are turned off, you can still advance into them with the `;` command; and if a breakpoint is placed in one, continuing with `c` will still stop on such breakpoints. In addition, once inside such a routine, the other debugger commands (`n`, `i`, `o`, `u`) will advance as normal inside of it; they won't immediately exit it.

### (h) print this help

Print the list of available commands.

### (q) quit

Quit the debugger.

### (r) reset

Reset the debugger to the beginning of the transaction.

### (b) set a breakpoint

This command allows you to set breakpoints for any line in any of your source files (see [examples](#adding-and-removing-breakpoints) below). These can be given by line number; by relative line number; by line number in a specified source file; or one may simply add a breakpoint at the current point in the code.

You don't need a transaction loaded to set breakpoints, although in that case you will have to specify which source file you mean to set it in.

### (B) remove a breakpoint

This command allows you to remove any of your existing breakpoints, with the same syntax as for adding them (see [example](#adding-and-removing-breakpoints) below). Type `B all` to remove all breakpoints.

### (c) continue until breakpoint

This command will cause execution of the code to continue until the next breakpoint is reached or the last line is executed.

### (:) evaluate and print expression

This command will evaluate and print the given expression, based on the current variables and their values (see also `v`).

### (+) add watch expression

This command will add a watch on a provided expression, based on the following syntax: `+:<expression>`.

### (-) remove watch expression

This command will remove a watch expression, based on the following syntax: `-:<expression>`.

### (?) list existing watch expressions and breakpoints

This command will display a list of all the current watch expressions and breakpoints. It will also report whether generated sources are turned on or off.

### (v) display variables

This command will display the current variables and their values.

### (T) unload transaction

This command unloads the current transaction so you can load a new one. Not usable in `--fetch-external` mode.

### (t) load transaction

This command loads a new transaction (given by its transaction hash). Note that if you already have a transaction loaded, you must first explicitly unload it before you can load a new one. Not usable in `--fetch-external` mode.

## 添加和删除断点

Below are some examples of adding and removing breakpoints. Note the difference in case between adding (a lowercase 'b') and removing (an uppercase 'B'). If you add a breakpoint at a place where the debugger will skip over, it will be automatically moved down to the next point that the debugger might stop. This does not apply to removing breakpoints. Use the `?` command to list current breakpoints.

```
MagicSquare.sol:

11:   event Generated(uint n);
12:
13:   function generateMagicSquare(uint n)
      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

debug(develop:0x91c817a1...)> b 23
Breakpoint added at line 23.

debug(develop:0x91c817a1...)> B 23
Breakpoint removed at line 23.

debug(develop:0x91c817a1...)> b SquareLib:5
Breakpoint added at line 5 in SquareLib.sol.

debug(develop:0x91c817a1...)> b +10
Breakpoint added at line 23.

debug(develop:0x91c817a1...)> b
Breakpoint added at this point in line 13.

debug(develop:0x91c817a1...)> B all
Removed all breakpoints.
```
