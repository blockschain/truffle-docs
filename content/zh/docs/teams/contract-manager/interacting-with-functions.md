---
title: 与功能进行交互
weight: 2
---

请注意，本文档的这一部分假定您已经部署了合同并导航到合同管理器。
如果您尚未这样做，请查看[合同管理器概述](/docs/teams/contract-manager/contract-manager-overview)了解更多详细信息。

To interact with a function, click on a function signature from the list of functions within the **Functions** section.
If the function accepts parameters, you'll see an input box for each parameter.
We accept valid YAML and/or JSON as inputs.

<figure class="screenshot">
  <img class="img-fluid" src="/img/docs/teams/contract-manager-02.png" title="Contract manager functions" alt="Contract manager functions" />
  <figcaption class="text-center">Contract manager functions</figcaption>
</figure>

### 使用结构作为参数

There are two different ways to input a struct as a parameter: as an array of values or as objects with the keys being the names of the struct fields.

For example, given this struct:

```javascript
struct Repository {
    string name;
    string[2] branches;
}
```

You can input the parameter as an array of values:

```javascript
["truffle-teams", ["main", "chore/update-readme"]];
```

Or you can input the parameter as an object:

```javascript
{
    name: "truffle-teams",
    branches: ["main", "chore/update-readme"]
}
```
