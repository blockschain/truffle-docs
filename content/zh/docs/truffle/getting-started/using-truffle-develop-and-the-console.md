---
title: 使用 Truffle 开发和控制台
weight: 12
---

有时候很高兴与您的合约交互式用于测试和调试目的，或者用手执行交易。
Truffle 通过交互式控制台为您提供两种简单的方法，并提供您的合约并准备使用。

- **Truffle Console**: 连接到任何 Ethereum 客户端的基本交互式控制台
- **Truffle Develop**: 一个交互式控制台，也会产生一个开发区块链

注意: 您的合约名称将作为变量加载到控制台上下文中。 因此，建议避免可能与节点的本机对象冲突的名称，如`Buffer`或`String`。 更新查看[GitHub 上的相关问题](https://github.com/trufflesuite/truffle/issues/3329).

## 为什么两个不同的控制台？

Having two different consoles allows you to choose the best tool for your needs.

使用 **Truffle Console** 的原因:

- 您有一个您已经使用的客户, 如 [Ganache](/docs/ganache/using) or geth
- 您希望迁移到 TestNet (或者主纪念网络)
- 您想使用特定的助记符或帐户列表

使用 **Truffle Develop** 的原因:

- 您正在测试您的项目，无需立即部署
- 您无需使用特定帐户 (使用默认开发帐户，您很好)
- 您不想安装和管理单独的区块链客户端

## 命令

所有命令都要求您在项目文件夹中。你不需要处于根目的。

### 安慰

启动控制台:

```shell
truffle console
```

This will look for a network definition called `development` in the configuration, and connect to it, if available. You can override this using the `--network <name>` option or [customize](/docs/truffle/reference/configuration#networks) the `development` network settings. See more details in the [Networks](/docs/advanced/networks) section as well as the [command reference](/docs/advanced/commands).

加载控制台时，您将立即看到以下提示:

```shell
truffle(development)>
```

This tells you you're running within a Truffle console using the `development` network.

### Truffle Develop

启动 Truffle Develop:

```shell
truffle develop
```

This will spawn a development blockchain locally on port `9545` by default. If you already have a `truffle develop` session running, it will instead connect to that development blockchain.

When you load Truffle Develop, you will see the following:

```shell
Truffle Develop started at http://localhost:9545/

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
```

This shows you the addresses, private keys, and mnemonic for this particular blockchain.

注意: When you run `truffle develop` for the first time, Truffle will generate a random mnemonic that will persist for you and you alone. If you want to use a different mnemonic or set of addresses, we recommend using [Ganache](/docs/ganache/using).

<p class="alert alert-danger">
Warning: Remember to never use any of these addresses or the mnemonic on the mainnet. This is for development only.

#### 日志 RPC 活动

If you wish to see information regarding RPC activity during your Truffle
develop session, you can use the `--log` option.

When you run `truffle develop --log`, Truffle will start up a new develop
session and output the addresses and keys as described in the previous section.
However, in this terminal window you will not be able to interact with the
console like you would in a normal Truffle develop session. Instead it will
only output the RPC activity occurring on the network. If
you want to interact with the console, you will have to open a new terminal
window and connect to the current session by running `truffle develop`.

If you already have a Truffle develop session running and want to log all
RPC activity occurring on it, you can run `truffle develop --log` in a
separate terminal window. It will then connect to that session
and act the same way as described above.

#### 配置 Truffle Develop

You can configure `truffle develop` to use any of the available
[ganache-core](https://github.com/trufflesuite/ganache-core#usage) options and [configurable](/docs/truffle/reference/configuration#networks) network settings.

For example:

```javascript
module.exports = {
  /* ... rest of config */

  networks: {
    /* ... other networks */

    develop: {
      port: 8545,
      network_id: 20,
      accounts: 5,
      defaultEtherBalance: 500,
      blockTime: 3,
    },
  },
};
```

## 特征

Both Truffle Develop and the console provide most of the features available in the Truffle command line tool. For instance, you can type `migrate --reset` within the console, and it will be interpreted the same as if you ran `truffle migrate --reset` on the command line.

Additionally, both Truffle Develop and the console have the following features:

- All of your compiled contracts are available and ready for use.
- After each command (such as `migrate --reset`) your contracts are reprovisioned so you can start using the newly assigned addresses and binaries immediately.
- The `web3` library is made available and is set to connect to your Ethereum client.

### 可用的命令

- `build`
- `compile`
- `create`
- `debug`
- `deploy`
- `exec`
- `help`
- `install`
- `migrate`
- `networks`
- `opcode`
- `publish`
- `run`
- `test`
- `version`

If a Truffle command is not available, it is because it is not relevant for an existing project (for example, `init`) wouldn't make sense (for example, `develop` or `console`).

See full [command reference](/docs/advanced/commands) for more information.
