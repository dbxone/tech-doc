# DBXChain api 调用逻辑
![](../../dbxchain.png)

由图可知，DBXChain主要有`dbxchain`、`dbxui`、`dbxfaucet`三大部分组成，各部分的基本介绍在此不再做赘述，具体请查阅[DBXChain构成](../../introduction.md)。

由图可知，api的调用逻辑可以分为两大主线进行区分，即`区块浏览`和`账户操作`。

`区块浏览`相关的功能调用，直接访问witness_node的api接口。
`账户操作`相关的功能调用，需要访问水龙头的api接口；水龙头再访问cli_wallet的api接口，cli_wallet最后再调用witness_node的api接口。

`web钱包`，主要有两部分功能，即区块浏览和在线账户注册。

`水龙头`，用于中间账户注册环节。

`命令行钱包`，cli_wallet程序，提供了多种api调用方式，

- `链核心模块` —— 全节点，即witness_node程序， 通过 P2P 方式连接到DBXChain网络，从网络接收最新区块，向网络广播本地签署的交易包。[witness_node 参数介绍](node/cmd/witness_node.md) 
<br>


