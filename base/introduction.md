# DBXChain构成

DBXChain主要有`dbxchain`、`dbxui`、`dbxfaucet`三大部分组成：

## [<b>dbxchain</b>](../dbxchain/introduction.md)

DBXChain公链，基于石墨烯技术，基于C++开发。

dbxchain主要由`链核心模块`和`轻钱包`程序组成。

- `链核心模块` —— 全节点，即witness_node程序， 通过 P2P 方式连接到DBXChain网络，从网络接收最新区块，向网络广播本地签署的交易包。

- `轻钱包` —— 也叫做命令行钱包，即cli_wallet程序， 通过 websocket 方式连接到 witness_node， 管理钱包文件； 提供交易签名功能，签名后通过 witness_node 向外广播； 通过 http rpc 的方式提供 API 供其他程序调用。

## [<b>dbxui</b>](dbxui_introduction.md) 

web在线钱包，区块浏览器，同时也是在线的钱包。web形式的浏览器客户端，基于Nodejs开发。

## [<b>dbxfaucet</b>](dbxfaucet_introduction.md) 

水龙头，用于web钱包客户端连接，继续宁账户注册服务，基于ruby开发。


# DBXChain网络模型
![](dbxchain.png)
