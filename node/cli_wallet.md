# 简单介绍

dbx轻钱包是一种`命令行钱包` —— 即cli_wallet程序， 通过 websocket 方式连接到 witness_node， 管理钱包文件； 提供交易签名功能，签名后通过 witness_node 向外广播； 通过 http rpc 的方式提供 API 供其他程序调用。

## 调用示例

命令行钱包cli_wallet连接witness_node:
```
cli_wallet -w wallet.json -s ws://127.0.0.1:38090 -r 127.0.0.1:38091 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```
首先需要为钱包设置一个钱包密码(这个密码是本地的，用来解锁钱包)：

```
new >>> set_password my_password
```

执行成功后会显示:
```
locked >>>
```

解锁钱包:
```
locked >>> unlock my_password
```

解锁成功会显示：
```
unlocked >>>
```

使用 info 命令可以查看当前区块同步情况
```
unlocked >>> info
info
{
  "head_block_num": 13845,
  "head_block_id": "000036155a3877d925a485a53c389337b526f6c5",
  "head_block_age": "0 second old",
  "next_maintenance_time": "6 minutes in the future",
  "chain_id": "6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d",
  "participation": "100.00000000000000000",
  "active_witnesses": [
    "1.6.1",
    "1.6.2",
    "1.6.3",
    "1.6.4",
    "1.6.5",
    "1.6.6",
    "1.6.7",
    "1.6.8",
    "1.6.9",
    "1.6.10",
    "1.6.11"
  ],
  "active_committee_members": [
    "1.5.0",
    "1.5.1",
    "1.5.2",
    "1.5.3",
    "1.5.4",
    "1.5.5",
    "1.5.6",
    "1.5.7",
    "1.5.8",
    "1.5.9",
    "1.5.10"
  ]
}
```


具体参数使用请查阅[cli_wallet 参数介绍](cmd/cli_wallet.md)
具体api使用请查阅[cli_wallet api 介绍](api/cli_wallet.md)