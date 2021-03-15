---
title: Drizzle 状态
weight: 2
---

```javascript
{
  accounts,
  accountBalances: {
    address
  }
  contracts: {
    contractName: {
      initialized,
      synced,
      events,
      callerFunctionName: {
        argsHash: {
          args,
          value
        }
      }
    }
  },
  currentBlock,
  drizzleStatus: {
    initialized
  },
  transactions: {
    txHash: {
      confirmations,
      error,
      receipt,
      status
    }
  },
  transactionStack,
  web3: {
    status
  }
}
```

## `accounts` (array)
An array of account addresses from `web3`.

## `accountBalances` (object)
An object whose keys are account addresses and values are account balances (in Wei).

## `contracts` (object)
A series of contract state objects, indexed by the contract name as declared in its ABI.

### `contractName` (object)

`initialized` (boolean): `true` once contract is fully instantiated.
`synced` (boolean): `false` if contract state changes have occurred in a block and Drizzle is re-running its calls.

`events` (array): An array of event objects. Drizzle will only listen for the events we declared in options.

The contract's state also includes the state of each constant function called on the contract (`callerFunctionName`). The functions are indexed by name, and contain the outputs indexed by a hash of the arguments passed during the call (`argsHash`). If no arguments were passed, the hash is `0x0`. Drizzle reads from the store for you, so it should be unnecessary to touch this data cache manually.

`args` (array): Arguments passed to function call.
`value` (mixed): Value returned from function call.

### `currentBlock` (object)
An object the latest block as an object resulting from [`web3.getBlock()`](https://web3js.readthedocs.io/en/1.0/web3-eth.html#getblock). This is updated once the block is received from a subscription or fetched via polling, but before any processing takes place.

## `drizzleStatus` (object)
An object containing information about the status of Drizzle.

`initialized` (boolean): `true` once:
*   `web3` is found or instantiated
*   Account addresses are stored in state
*   All contracts are instantiated

### `initialized` (boolean)
`false` by default, becomes true once a `web3` instance is found and the accounts and contracts are fetched.

## `transactions` (object)
A series of transaction objects, indexed by transaction hash.

### `txHash` (object)

`confirmations` (array): After the initial receipt, further confirmation receipts (up to the 24th).
`error` (object): contains the returned error if any.
`receipt` (object): contains the first transaction receipt received from a transaction's `success` event.

`status` (string): `true` or `false` depending on transaction status
*   `pending` when the transaction has broadcasted successfully, but is not yet mined
*   `success` when a transaction receipt has been received (you may also wish to check for further confirmations)
*   `error` if any errors occurred after broadcasting

For more in-depth information on the Ethereum transaction lifecycle, [check out this great blog post](https://medium.com/blockchannel/life-cycle-of-an-ethereum-transaction-e5c66bae0f6e).

## `transactionStack` (array)
In cases where a user cancels a transaction or the transaction is malformed and unable to be broadcasted, it won't receive a hash. To keep track of these cases, a temporary ID will be added to this array and replaced with the transaction hash once broadcasted. The `cacheSend()` method will return a `stackId`, which will allow you get the temporary ID to observe this process for your own transaction status indicator UI.

## `web3` (object)

`status` (string): `initializing`, `initialized` and `failed` are possible options. Useful for triggering warnings if `web3` fails to instantiate.