---
title: 3种方式企业正在解决区间的隐私问题
date: 2019-07-31
author: Danny Pan, Guest Blogger, West Monroe Partners
published: true
description: >
---

今年已经看到了财富 500 强的单一和多党组区块飞行员的众多公告，例如...星巴克和 Metlife。
数据隐私问题并没有阻止他们，企业区块链世界已经采取了这些步骤来改变他们的思考。

[BlockChain 被吹捧为伟大的连接器，以在联盟网络下整合业务](https://www.forbes.com/sites/andrewarnold/2019/02/21/why-2019-may-become-the-year-of-enterprise-blockchain/#66c9e516427e).
它能够验证使用智能合约的数据，并通过不可变共享数据跨网络参与者提供透明度，让人们谈论技术革命。
然而，这种好处是一把双刃剑，因为企业世界对在无法删除信息的分类帐上分享敏感数据持怀疑态度。
好消息是，今年已经看到了财富 500 强的单一和多党组区块飞行员的众多公告，如...... [星巴克](https://news.microsoft.com/transform/starbucks-turns-to-technology-to-brew-up-a-more-personal-connection-with-its-customers/) and [MetLife](https://www.forbes.com/sites/stevenehrlich/2019/06/19/metlife-plans-to-disrupt-2-7-trillion-life-insurance-industry-using-ethereum-blockchain/#3e9a87277022).
数据隐私问题并没有阻止他们，企业区块链世界已经采取了这些步骤来改变他们的思考。

## 1. 存储对区块链上的数据的引用

规避此数据隐私问题的最简单方法是不会将数据放在链上。
一种流行的方法是在区块链上共享匿名 ID，并使用它从另一个系统获取数据。 For example, [MediLedger](https://www.mediledger.com/) is a supply chain pilot in the heavily regulated pharmaceutical industry that uses a blockchain to trace a drug’s exchange of hands and then uses another private peer-to-peer application to transfer details about the medication. What is passed around on the chain is just an anonymous identifier to the medication. This keeps transactions light, allows enterprises to regulate data access, and uses proven methods to secure sensitive data. MediLedger actually takes this a step further and anonymizes the transaction details with zero knowledge proofs — which I’ll cover later.

## 2. 使用 blockchains 验证而不是共享

Blockchain’s real power is in its ability to verify data. Instead of putting actual information on the chain, a solution could combine unique elements of data and share a hash of it on the blockchain. Hashing is a cryptographic method that generates a random, unique value from a fed input. In this scenario, the resulting hash itself doesn’t reveal any information, but it can verify an on-hand document by checking if it generates the same hash when fed into the function. The data inputs could also be selected in a way that no critical information is sampled to create the hash so that compliance regulations can be withheld. Businesses have reliable methods to exchange data, but the verification is long and expensive. By using blockchain as a verifier and not the store of the data, we can ease the pain point and maintain a higher level of privacy than open sharing.

## 3. 匿名交易具有零知识证明

Building off the two previous trends, blockchain pilots have taken an extra step in securing data and replaced hashed transaction details with zero knowledge proofs (ZKP). [ZKPs allow for verification of a transaction without exposing transaction details](https://hackernoon.com/wtf-is-zero-knowledge-proof-be5b49735f27). Now two businesses can communicate on a public network and be completely anonymous. This is because what is placed on the chain is a proof that is cryptographically verified by the receiver, not the data that goes into the transaction. This shift in data validation methods addresses data privacy concerns and supports industry consortiums.

## 区块链只是一件拼图

Finally, with all the hype on blockchain’s potential in the last years, we have to remember that this is just another tool in the technology box when solving a problem. Enterprises have gotten smarter in finding ways to use blockchain to solve unique problems that are more expensive or less reliable with other technologies. What we have seen is that distributed ledgers can’t do everything, but when paired with multiple other technologies that help fill gaps, the solution as a whole is optimized. A better perspective is to not think of future solutions as blockchain applications, but rather applications that leverage the unique advantages of blockchain.

## 关于西门德罗合作伙伴

West Monroe is a national business and technology consulting firm that partners with dynamic organizations to reimagine, build, and operate their businesses at peak performance. Our team of more than 1,400 professionals across nine offices is comprised of an uncommon blend of business consultants and deep technologists. I am one of those consultants and I am one of the leaders of our blockchain center of excellence. I’ll be presenting on Sunday morning (8/4) about one of our blockchain projects that looks to [incentivize electric vehicle owners to charge with cleaner energy](https://trufflecon2019.sched.com/event/RHIR/driving-renewable-energy-usage-with-blockchain-and-electric-vehicles). Check us out at our [website](https://www.westmonroepartners.com/) and read more about our [blockchain perspectives](https://blog.westmonroepartners.com/?s=blockchain) on our blog!

Danny Pan is a consultant with West Monroe Partner’s Seattle Technology Practice. He focuses on providing value in adopting blockchain, distributed technologies, and robust SDLC practices. Contact Danny at [dpan@wmp.com](mailto:dpan@wmp.com)
