---
title: 与您的合约互动
weight: 5
---

## 介绍

如果您自己向 Ethereum 网络写入原始请求，以便与您的合约互动, 你很快就会意识到写这些请求是笨拙和繁琐的。
同样，您可能会发现管理您所做的每个请求的状态 _complicated_.
幸运的是， Truffle 对你负责这种复杂性，与您的合约进行互动。

## 读写数据

Ethereum Network 将数据写入网络和从中读取数据的区分， 而且这种区别在您如何编写应用程序中发挥了重要作用.
通常，写入数据被称为 **transaction** 虽然读取数据被称为 **call**.
transaction 和 call 是非常不同的，并具有以下特征.

### Transactions

transaction 从根本上改变了网络的状态.
transaction 可以像向其他帐户发送以太网一样简单，或者作为执行合约函数或向网络添加新合约的复杂性.
transaction 的定义特征是它写入（或更改）数据.
transaction 运行成本以太，已知为 "gas", transaction 需要时间来处理.
当您通过 transaction 执行合约函数时, 您无法收到该函数的返回值，因为 transaction 未立即处理.
通常，通过 transaction 执行的功能意味着不会返回值;它们将返回 transactionID。
所以总之，transaction:

- 成本 gas (Ether)
- 改变网络的状态
- 没有立即处理
- 不会公开返回值（仅 transactionID）.

### Calls

另一方面，call 是非常不同的。
调用可用于在网络上执行代码，但没有数据将永久更改。
call 可以自由运行，并且它们定义特征是他们读取数据。
通过 call 执行合约函数时，您将立即收到返回值。
总之，call:

- 免费 (不要花费天然气)
- 不要改变网络的状态
- 立即加工
- 将揭露退货值 (赫雷!)

选择 transaction 和 call 之间的简单正义决定是否要读取数据，或写入。

## 介绍抽象

合约抽象是与 JavaScript 与 Ethereum 合约互动的面包和黄油。
简而言之，合约抽象是包装代码，使您的合约互动，以便让您忘记在引擎盖下执行的许多发动机和齿轮。
Truffle 通过自己的[@truffle/contract](https://github.com/trufflesuite/truffle/tree/master/packages/contract) 模块合约抽象 ,这是此合约抽象，如下所述.

然而，为了欣赏合约抽象的有用性，我们首先需要合约谈谈。
我们将使用它 MetaCoin 合约 适用于您 通过 Truffle 盒子 通过 `truffle unbox metacoin`.

```solidity
pragma solidity >=0.4.25 <0.6.0;

import "./ConvertLib.sol";

// This is just a simple example of a coin-like contract.
// It is not standards compatible and cannot be expected to talk to other
// coin/token contracts. If you want to create a standards-compliant
// token, see: https://github.com/ConsenSys/Tokens. Cheers!

contract MetaCoin {
	mapping (address => uint) balances;

	event Transfer(address indexed _from, address indexed _to, uint256 _value);

	constructor() public {
		balances[tx.origin] = 10000;
	}

	function sendCoin(address receiver, uint amount) public returns(bool sufficient) {
		if (balances[msg.sender] < amount) return false;
		balances[msg.sender] -= amount;
		balances[receiver] += amount;
		emit Transfer(msg.sender, receiver, amount);
		return true;
	}

	function getBalanceInEth(address addr) public view returns(uint){
		return ConvertLib.convert(getBalance(addr),2);
	}

	function getBalance(address addr) public view returns(uint) {
		return balances[addr];
	}
}
```

这份合约除了构造函数之外有三种方法 (`sendCoin`, `getBalanceInEth`, 和 `getBalance`).
所有三种方法都可以作为 transaction 或 call 执行.

现在让我们看看由 Truffle 提供给我们的名为`MetaCoin`的 JavaScript 对象, 如[Truffle Console](/docs/truffle/getting-started/using-truffle-develop-and-the-console)所提供的:

```javascript
truffle(develop)> let instance = await MetaCoin.deployed()
truffle(develop)> instance

// outputs:
//
// Contract
// - address: "0xa9f441a487754e6b27ba044a5a8eb2eec77f6b92"
// - allEvents: ()
// - getBalance: ()
// - getBalanceInEth: ()
// - sendCoin: ()
// ...
```

请注意，抽象包含合约中存在的完全相同的功能。
它还包含一个地址，该地址指向 Metacoin 合约的已部署版本。

## 执行合约功能

使用抽象可以轻松地在 Ethereum 网络上执行合约功能。

### 执行 transaction

在 Metacoin 合约上有三种功能，我们可以执行。
如果您分析它们，您将看到 `sendCoin` 是唯一旨在对网络进行更改的函数.
“sendcoin`的目标是 从一个帐户"send"到下一个帐户的一些元币, 这些变化应该持续存在.

在呼唤时 `sendCoin`, 我们将作为 transaction 执行它.
在以下示例中，我们将以一个帐户从一个帐户发送 10 个 Meta 硬币，以一种持续存在于网络的变化:

```javascript
truffle(develop)> let accounts = await web3.eth.getAccounts()
truffle(develop)> instance.sendCoin(accounts[1], 10, {from: accounts[0]})
```

关于上面的代码有一些有趣的事情:

- 我们称之为抽象的`sendcoin`功能. 这将导致默认(i.e, 写数据)情况而不是 call 的 transaction.
- 我们将一个物体作为第三个参数传递给`sendcoin`.请注意，我们坚持合约中的`Sendcoin`功能没有第三个参数. 您上面所看到的是一个特殊对象，可以始终作为最后一个参数传递给函数，允许您编辑有关 transaction 的特定详细信息 ("transaction params"). 在这里，我们设置了 `from` 地址 确保此 transaction 来自`accounts[0]`. 您可以设置的 transaction 参数对应于 Etereumtransaction 中的字段:
  - `from`
  - `to`
  - `gas`
  - `gasPrice`
  - `value`
  - `data`
  - `nonce`

### 执行 call

Continuing with MetaCoin, notice the `getBalance` function is a great candidate for reading data from the network. It doesn't need to make any changes, as it just returns the MetaCoin balance of the address passed to it. Let's give it a shot:

```javascript
truffle(develop)> let balance = await instance.getBalance(accounts[0])
truffle(develop)> balance.toNumber()
```

What's interesting here:

- We received a return value. Note that since the Ethereum network can handle very large numbers, we're given a [BN](https://github.com/indutny/bn.js/) object which we then convert to a number.

<p class="alert alert-warning">
Warning: We convert the return value to a number because in this example the numbers are small. However, if you try to convert a BN that's larger than the largest integer supported by Javascript, you'll likely run into errors or unexpected behavior.

### 处理 transaction 结果

When you make a transaction, you're given a `result` object that gives you a wealth of information about the transaction.

```javascript
truffle(develop)> let result = await instance.sendCoin(accounts[1], 10, {from: accounts[0]})
truffle(develop)> result
```

Specifically, you get the following:

- `result.tx` _(string)_ - Transaction hash
- `result.logs` _(array)_ - Decoded events (logs)
- `result.receipt` _(object)_ - Transaction receipt (includes the amount of gas used)

For more information, please see the [README](https://github.com/trufflesuite/truffle/tree/master/packages/contract) in the `@truffle/contract` package.

### 抓取事件

Your contracts can fire events that you can catch to gain more insight into what your contracts are doing. The easiest way to handle events is by processing the `logs` array contained within `result` object of the transaction that triggered the event.

If we explicitly output the first log entry we can see the details of the event that was emitted as part of the `sendCoin` call (`Transfer(msg.sender, receiver, amount);`).

```javascript
truffle(develop)> result.logs[0]
{ logIndex: 0,
  transactionIndex: 0,
  transactionHash: '0x3b33960e99416f687b983d4a6bb628d38bf7855c6249e71d0d16c7930a588cb2',
  blockHash: '0xe36787063e114a763469e7dabc7aa57545e67eb2c395a1e6784988ac065fdd59',
  blockNumber: 8,
  address: '0x6891Ac4E2EF3dA9bc88C96fEDbC9eA4d6D88F768',
  type: 'mined',
  id: 'log_3181e274',
  event: 'Transfer',
  args:
   Result {
     '0': '0x8128880DC48cde7e471EF6b99d3877357bb93f01',
     '1': '0x12B6971f6eb35dD138a03Bd6cBdf9Fc9b9a87d7e',
     '2': <BN: a>,
     __length__: 3,
     _from: '0x8128880DC48cde7e471EF6b99d3877357bb93f01',
     _to: '0x12B6971f6eb35dD138a03Bd6cBdf9Fc9b9a87d7e',
     _value: <BN: a> } }
```

### 向网络添加新合约

In all of the above cases, we've been using a contract abstraction that has already been deployed. We can deploy our own version to the network using the `.new()` function:

```javascript
truffle(develop)> let newInstance = await MetaCoin.new()
truffle(develop)> newInstance.address
'0x64307b67314b584b1E3Be606255bd683C835A876'
```

### 在特定地址使用合约

If you already have an address for a contract, you can create a new abstraction to represent the contract at that address.

```javascript
let specificInstance = await MetaCoin.at("0x1234...");
```

### 发送以太合约

You may simply want to send Ether directly to a contract, or trigger a contract's [fallback function](http://solidity.readthedocs.io/en/develop/contracts.html#fallback-function). You can do so using one of the following two options.

Option 1: Send a transaction directly to a contract via `instance.sendTransaction()`. This is promisified like all available contract instance functions, and has the same API as `web3.eth.sendTransaction` but without the callback. The `to` value will be automatically filled in for you if not specified.

```javascript
instance.sendTransaction({...}).then(function(result) {
  // Same transaction result object as above.
});
```

Option 2: There's also shorthand for just sending Ether directly:

```javascript
instance.send(web3.utils.toWei(1, "ether")).then(function (result) {
  // Same result object as above.
});
```

### Truffle 合约对象的特殊方法

There are a couple of special functions that you can find on the actual contract
methods of your contract abstractions:

- `estimateGas`
- `sendTransaction`
- `call`
- `request`

The first special method mentioned above is the `estimateGas` method. This, as you
probably can guess, estimates the amount of gas that a transaction will require.
If we wanted to estimate the gas for a transaction, we would call it on the
contract method itself. It would look something like the following:

```javascript
const instance = await MyContract.deployed();
const amountOfGas = await instance.sendTokens.estimateGas(4, myAccount);
```

This will give us an estimate of how much gas it will take to run the
transaction specified.

Note that the arguments above (`4` and `myAccount`) correspond to whatever the
signature of the contract method happens to be.

Another useful thing to note is that you can also call this on a contract's
new method to see how much gas it will take to deploy. So you would do
`Contract.new.estimateGas()` to get the gas estimate for the contract's deployment.

The next mentioned method is `sendTransaction`. In general, if you execute a
contract method, Truffle will intelligently figure out whether it needs
to make a transaction or a call. If your function can be executed
as a call, then Truffle will do so and you will be able to avoid gas costs.

There may be some scenarios, however, where you want to force Truffle to
make a transaction. In these cases, you can use the `sendTransaction`
method found on the method itself. This would look something
like `instance.myMethod.sendTransaction()`.

For example, suppose I have a contract instance with the method
`getTokenBalance`. I could do the following to force a transaction to take
place while executing `getTokenBalance`:

```javascript
const instance = await MyContract.deployed();
const result = await instance.getTokenBalance.sendTransaction(myAccount);
```

The `result` variable above will be the same kind of result you would get
from executing any normal transaction in Truffle. It will contain the
transaction hash, the logs, etc.

The next method is `call` and the syntax is exactly the same as for
`sendTransaction`. If you want to explicitly make a call, you can
use the `call` method found on your contract abstraction's method. So you
would write something that looks like
`const result = await instance.myMethod.call()`.

The last method is `request`. This method does not perform a transaction or
call, but rather returns an object that can be passed to
`web3.eth.sendTransaction` or `web3.eth.call` if you want to perform the
transaction or call yourself. It has the same syntax as the others, and
like with `estimateGas`, you can also do `Contract.new.request()` if you
want to perform a manual deployment.

### 调用重载方法

The current implementation of Truffle's contract abstraction can mistakenly
infer the signature of an overloaded method even though it exists in the
contract ABI.

Therefore, some methods may not be accessible through the contract's
instance, but their accessors can be invoked explicitly via the `.methods`
property of the contract.

```javascript
const instance = await MyContract.deployed();
instance.methods["setValue(uint256)"](123);
instance.methods["setValue(uint256,uint256)"](11, 55);
```

Please see this issue [here](https://github.com/trufflesuite/truffle/issues/2868) for more information.

### 使用枚举

Contract abstractions can also be used to access Solidity enumerations defined
within that contract. For instance, suppose we have the following Solidity contract:

```solidity
contract ExampleContract {
  enum ExampleEnum {
    ExampleOption0,
    ExampleOption1,
    ExampleOption2
  }

  // ...
}
```

One could then use `ExampleContract.ExampleEnum.ExampleOption0` to access that enum
value; in this case, that is equal to `0`, but using this allows one to pass in enums
to contract methods without having to worry about their numerical value.

A contract's enums are also available under `.enums`, so in this case, one could also
write `ExampleContract.enums.ExampleEnum.ExampleOption0`.

## 进一步阅读

The contract abstractions provided by Truffle contain a wealth of utilities for making interacting with your contracts easy. Check out the [@truffle/contract](https://github.com/trufflesuite/truffle/tree/master/packages/contract) documentation for tips, tricks and insights.
