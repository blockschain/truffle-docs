---
title: 写外部脚本/命令插件
weight: 11
---

通常，您可能想要运行与您的合同交互的外部脚本。 
Truffle提供了一种简单的方法，根据您的期望网络引导您的合同，并根据您的[项目配置](/docs/advanced/configuration)自动连接到Ethereum客户端.

## 命令

要运行外部脚本，请执行以下操作:

```shell
$ truffle exec <path/to/file.js>
```

有关此命令的更多信息，请参阅[Truffle命令参考](/docs/truffle/reference/truffle-commands#exec)，例如它接受的选项。

## 文件结构

为了正确运行外部脚本，Truffle希望它们导出将单个参数作为回调的函数导出:

```javascript
module.exports = function(callback) {
  // perform actions
}
```

您可以在此脚本中执行任何您想要的任何操作，只要在脚本完成时调用回调. 
回调接受错误作为其第一个也是唯一的参数. 
如果提供错误，则执行将停止，并且该过程将返回非零退出代码.


## 第三方插件命令

<p class="alert alert-warning">
<strong>Note</strong>: 此功能是新的，仍处于鞍状态。请告诉我们我们如何改进它！
</p>

## 插件安装/使用

1. 从NPM安装插件.
   ```shell
   npm install --save-dev truffle-plugin-hello
   ```

2. 添加一个 <code>plugins</code> 部分到Truffle Config.
   ```javascript
   module.exports = {
     /* ... rest of truffle-config */

     plugins: [
       "truffle-plugin-hello"
     ]
   }
   ```

3. Run the command
   ```shell
   $ truffle run hello
   Hello, World!
   ```


## 创建自定义命令插件

1. Implement the command as a Node module with a function as its default export.

   Example: `hello.js`

   ```javascript
   /**
    * Outputs `Hello, World!` when running `truffle run hello`,
    * or `Hello, ${name}` when running `truffle run hello [name]`
    * @param {Config} config - A truffle-config object.
    * Has attributes like `truffle_directory`, `working_directory`, etc.
    */
   module.exports = async (config) => {
     // config._ has the command arguments.
     // config_[0] is the command name, e.g. "hello" here.
     // config_[1] starts remaining parameters.
     if (config.help) {
       console.log(`Usage: truffle run hello [name]`);
       return;
     }

     let name = config._.length > 1 ? config._[1] : 'World!';
     console.log(`Hello, ${name}`);
   }
   ```

2.  定义一个`truffle-plugin.json`文件以指定命令。
    例子: <code>truffle-plugin.json</code>

    ```json
    {
      "commands": {
        "hello": "hello.js"
      }
    }
    ```

3.  发布到NPM.

    ```shell
    npm publish
    ```

## 将松露作为模块

```javascript
const truffle = require("truffle");
```

从`v5.0.30开始， Truffle导出[core / index.js]中列出的方法(https://github.com/trufflesuite/truffle/blob/develop/packages/core/index.js). 
这意味着您的插件可以将用户的Truffle实例作为库，并访问其内部命令API的子集。

如果您需要连续触摸多个Truffle命令，则这些非常有用。 
例如，想象一个插件，它评估了在不同级别的Solc优化水平上进行的合同系统。 
它的工作流程可能看起来像:
```
for a range of solc settings:
   compile contracts to a temp folder
   run user's tests using the temp artifacts
   measure and save gas usage data

aggregate data and report
```
Truffle Library允许您执行此操作，而无需使用户将其自己的命令添加在一起。

:warning: **Important Note** :warning:

Truffle不保证其内部API将遵循明星。 
您应该为您的用户准备好运行任何块状版本并优雅地处理不匹配。 
通过使用图书馆 **you are entering into a gentleperson's agreement** 代表用户管理API波动率和其他突发事件. 
一些技巧:

+ 总是在一个 try/catch 块 `require` Truffle 
+ 在运行时，验证您需要的API组件实际暴露
+ 尽可能消耗单独发布（和emver保证）Truffle模块
+ 将自己添加到Github上的Truffle repo观看列表中，并及时了解可能影响您的内部变化。
+ 不要去度假






