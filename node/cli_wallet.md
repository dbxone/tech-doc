# 简单介绍

dbx轻钱包是一种`命令行钱包` —— 即cli_wallet程序， 通过 websocket 方式连接到 witness_node， 管理钱包文件； 提供交易签名功能，签名后通过 witness_node 向外广播； 通过 http rpc 的方式提供 API 供其他程序调用。


具体参数使用请查阅[cli_wallet 参数介绍](cmd/cli_wallet.md)
具体api使用请查阅[cli_wallet api 介绍](api/cli_wallet.md)