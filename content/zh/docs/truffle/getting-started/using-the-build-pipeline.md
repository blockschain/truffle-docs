---
title: 使用构建管道
weight: 10
---

<p class="alert alert-warning">
<strong>警报</strong>: 此命令已不推荐使用。 请使用像webpack或grunt这样的第三方构建工具，或看我们的 <a href="/boxes">Truffle Boxes</a> 对于一个例子.
</p>

Truffle 1.0 and 2.0 came standard with a default build system heavily geared toward web applications (here, the term "build" means turning code artifacts into HTML, Javascript and CSS). That build system has been pulled out into its [own module](https://github.com/trufflesuite/truffle-default-builder/tree/master) to make Truffle usable and extensible for all kinds of applications.

Truffle can be configured for tight integration with any build system. To configure a custom build system, see the [Advanced Build Processes](/docs/advanced/build_processes) section for more details.

## 命令

配置构建系统时构建应用程序，运行:

```shell
$ truffle build
```

注意如果您尝试运行`build`命令，则会收到错误，而无需先配置自定义构建过程。
