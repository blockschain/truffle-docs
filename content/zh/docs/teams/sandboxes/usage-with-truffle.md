---
title: 使用 Truffle 的用法
linkTitle: 使用Truffle
weight: 5
---

您可以使用与 Ganache 一起使用的所有 Truffle 命令的沙箱，包括: `migrate`, `console`, and `test`!
使用 Truffle 版本 v5.1.28 及更高版本，使用沙箱只需要`url`字段:

```javascript
module.exports = {
  networks: {
    teams: {
      url:
        "https://sandbox.truffleteams.com/ac98e539-140d-498e-818e-8284eee9d933",
      network_id: 1583853263114,
    },
  },
};
```

如果您正在使用旧版本的 Truffle，则需要使用 HDWalletProvider。
除了提供 `mnemonic` 和 `network_id`, 我们必须指定初始帐户索引 (`0`), 账户总数 (`10`), 并设置`shareNonce`选项 `false`.
这是一个完整的例子:

```javascript
const HDWalletProvider = require("@truffle/hdwallet-provider");
const teamsMnemonic =
  "custom buzz situate mesh cannon number grass improve iron swim pilot cool";

module.exports = {
  networks: {
    teams: {
      provider: function () {
        return new HDWalletProvider(
          teamsMnemonic,
          "https://sandbox.truffleteams.com/ac98e539-140d-498e-818e-8284eee9d933",
          0,
          10,
          false
        );
      },
      network_id: 1583853263114,
    },
  },
};
```
