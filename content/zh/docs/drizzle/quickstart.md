---
title: 快速开始
weight: 2
---

## 安装

通过 NPM 安装 Drzzle：

```shell
npm install --save @drizzle/store
```

**Using React?**: The easiest way to get started with Drizzle is to use our [official `@drizzle/react-plugin` package](https://github.com/trufflesuite/drizzle/tree/master/packages/react-plugin) and (optionally) its [companion `@drizzle/react-components`](https://github.com/trufflesuite/drizzle/tree/master/packages/react-components).

## 初始化

<p class="alert alert-info m-t-2">
注意: Since Drizzle uses web3 1.0 and web sockets, be sure your development environment can support these. As a development blockchain, you'll need `ganache-cli` v6.1.0+, `geth` or `parity`.

1. Import the provider.

   ```javascript
   import { Drizzle } from "@drizzle/store";
   ```

1. Create an `options` object and pass in the desired contract artifacts for Drizzle to instantiate. Other options are available, see [the Options section](./reference/drizzle-options).

   ```javascript
   // Import contracts
   import SimpleStorage from "./../build/contracts/SimpleStorage.json";
   import TutorialToken from "./../build/contracts/TutorialToken.json";

   const options = {
     contracts: [SimpleStorage],
   };

   const drizzle = new Drizzle(options);
   ```

<p class="alert alert-info m-t-2">
注意: The above assumes you have no existing redux store and generates a new one. To use your existing redux store, see [Using an Existing Redux Store](./getting-started/using-drizzles-redux-store).
