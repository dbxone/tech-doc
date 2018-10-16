# DBXChain简介

DBXChain是一条公有链，是DBXChain数据交易所的底层区块链，不仅支撑着DBXChain的高频数据交易，还支持第三方开发应用，在DBXChain上开发应用不仅可以得到链上支持，还可以获得DBXChain多维度数据的对接，可以做出非常落地于民生的有价值应用。

* [编译安装](compile.md)
* [搭建私链](private-chain.md)
* [witness_node参数介绍](witness_node.md)
* [cli_wallet参数介绍](cli_wallet.md)

DBXChain主要有dbx-core、dbxui、dbxfaucet三大部分组成：

* [dbx-core](dbxchain_introduction.md)

DBXChain公链，基于石墨烯技术，基于C++开发。

dbxchain主要由witness_node和cli_wallet程序组成。

witness_node 通过 P2P 方式连接到DBXChain网络，从网络接收最新区块，向网络广播本地签署的交易包。

cli_wallet 通过 websocket 方式连接到 witness_node， 管理钱包文件； 提供交易签名功能，签名后通过 witness_node 向外广播； 通过 http rpc 的方式提供 API 供其他程序调用。

主网接入点地址: <b>`ws://mainnet.dbxchain.io`</b><br>
测试网接入点地址: <b>`ws://testnet.dbxchain.io`</b>

* [dbxui](dbxui_introduction.md) 

web在线钱包，区块浏览器，同时也是在线的钱包。web形式的浏览器客户端，基于Nodejs开发。

主网在线钱包地址: <b> http://wallet.mainnet.dbxchain.io</b> <br>
测试网在线钱包地址: <b> http://wallet.testnet.dbxchain.io</b>


* [dbxfaucet](dbxfaucet_introduction.md) 

水龙头，用于web钱包客户端连接，继续宁账户注册服务，基于ruby开发。

主网水龙头地址: <b> https://wallet.mainnet.dbxchain.io/account/register</b> <br>
测试网水龙头地址: <b> https://wallet.testnet.dbxchain.io/account/register</b>
