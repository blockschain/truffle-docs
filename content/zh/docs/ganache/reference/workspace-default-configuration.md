---
title: 工作区默认配置
weight: 2
---

每个工作区都有自己的配置。
每个工作空间的配置均基于工作空间创建时的快速入门配置。
虽然可以更改这些内容，但`Quickstart`工作区从以下选项开始:

## Ethereum

```
Hostname: 127.0.0.1 - localhost
Port Number: 7545
Network ID: 5777
Automine: true
Error on Tx Failure: true

Account Default Balance: 100
Total Accounts to Generate: 10
Autogenerate HD Mnemonic: false
Lock Accounts: false

Output Logs to File: false
Verbose Logs: false
```

但是，在创建工作空间期间，`Autogenerate HD Mnemonic`设置为`true`以维护相同的帐户组。

## Corda

```
Postgres Port: 15432
Projects: []
Nodes: 3
Notaries: 1
Node 1:
  Name: O=Party A,L=London,C=GB
  RPC Port: 10000
  Admin Port: 10001
  P2P Port: 10002
  CordApps: []
  Nodes: [
    O=Party B,L=Paris,C=FR
    O=Party C,L=New York,C=US
  ]
  SSHD Port: 11000
  Version: 4.4
Node 2:
  Name: O=Party B,L=Paris,C=FR
  RPC Port: 10003
  Admin Port: 10004
  P2P Port: 10005
  CordApps: []
  Nodes: [
    O=Party A,L=London,C=GB
    O=Party C,L=New York,C=US
  ]
  SSHD Port: 11003
  Version: 4.4
Node 3:
  Name: O=Party C,L=New York,C=US
  RPC Port": 10006
  Admin Port: 10007
  P2P Port: 10008
  CordApps: []
  Nodes: [
    O=Party A,L=London,C=GB
    O=Party B,L=New York,C=US
  ],
  SSHD Port: 11006
  Version: 4.4
Notary 1:
  Name: O=Notary Service,L=London,C=GB
  RPC Port: 10009
  Admin Port: 10010
  P2P Port: 10011
  CordApps: []
  SSHD Port: 11009
  Version: 4.4
```
