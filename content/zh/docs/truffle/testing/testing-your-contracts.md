---
title: 测试您的合同
weight: 1
---

## 框架

松露来标配自动化测试框架，以便测试您的合约微风。 
此框架允许您以两种不同的方式编写简单和可管理的测试:

* In [Javascript](/docs/getting_started/javascript-tests) and [TypeScript](/docs/getting_started/javascript-tests#typescript-file-support), for exercising your contracts from the outside world, just like your application.
* In [Solidity](/docs/getting_started/solidity-tests), for exercising your contracts in advanced, bare-to-the-metal scenarios.

这两种测试都有其优点和缺点。 
有关每个人的讨论，请参阅接下来的两个部分。

## 位置

All test files should be located in the `./test` directory. Truffle will only run test files with the following file extensions: `.js`, `.ts`, `.es`, `.es6`, and `.jsx`, and `.sol`. All other files are ignored.

## 命令

To run all tests, simply run:

```shell
$ truffle test
```

Alternatively, you can specify a path to a specific file you want to run, e.g.,

```shell
$ truffle test ./path/to/test/file.js
```

## 洁净室环境

Truffle在运行测试文件时提供干净的房间环境。 
在以[GANACHE](/ganache)或TROUFALLE开发的测试时, Truffle将使用高级快照功能，以确保您的测试文件不会彼此共享状态. 
当跑到其他以外的客户端时，如[Go-Ethereum](https://github.com/ethereum/go-ethereum), Truffle将在每个测试文件的开头重新部署所有迁移，以确保您有一套新的合同来测试。

## 速度和可靠性考虑

Both Ganache and Truffle Develop are significantly faster than other clients when running automated tests. Moreover, they contain special features which Truffle takes advantage of to speed up test runtime by almost 90%. As a general workflow, we recommend you use Ganache or Truffle Develop during normal development and testing, and then run your tests once against go-ethereum or another official Ethereum client when you're gearing up to deploy to live or production networks.

## 堆栈痕迹

You can obtain Solidity stack traces for failed transactions with `truffle test --stacktrace`.  This will produce stack traces for transactions and deployments made via Truffle Contract during your tests should one of them revert and thereby causes your test to fail.  This option is still experimental, and stack traces are not currently supported for calls or gas estimates.  Moreover, while it is turned on, `PromiEvent` functionality of Truffle Contract (as opposed to `Promise` functionality) may not work.

There is also the option `truffle test --stacktrace-extra`.  This will turn on stack traces and will additionally compile contracts in Solidity's debug mode for additional revert messages.  This debug mode was only introduced in Solidity 0.6.3 so it will have no effect on earlier versions of Solidity.  Using debug mode may cause problems on larger contracts.
