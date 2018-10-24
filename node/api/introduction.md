# DBXChain api 调用逻辑
![](../../dbxchain.png)

由图可知，DBXChain主要有`dbxchain`、`dbxui`、`dbxfaucet`三大部分组成，各部分的基本介绍在此不再做赘述，具体请查阅[DBXChain构成](../../introduction.md)。

由图可知，api的调用逻辑可以分为两大主线进行区分，即`区块浏览`和`账户操作`。

- `区块浏览`相关的功能调用，直接访问witness_node的api接口。
- `账户操作`相关的功能调用，需要访问水龙头的api接口；水龙头再访问cli_wallet的api接口，cli_wallet最后再调用witness_node的api接口。需要注意的是，DBXChain系统中的账户注册，可以通过`终身账户`(相关介绍请查阅[搭建私链](../private-chain.md))注册的，链上的某个`终身账户`已经在cli_wallet钱包中已经加载，因此可以为水龙头和web钱包提供账户注册服务。并且在账户注册时，为新账户注册提供了一定的手续费。


因此，可以对api进行分类，分别为witness_node的`链api`、cli_wallet的`钱包api`和水龙头的`水龙头api`。

