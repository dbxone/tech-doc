# 部署DBXChain节点


DBXChain节点介绍
---------------

DBXChain节点主要包含witness\_node和cli\_wallet两部分。

witness\_node 通过 P2P 方式连接到DBXChain网络，从网络接收最新区块，向网络广播本地签署的交易包。

cli\_wallet 通过 websocket 方式连接到 witness\_node， 管理钱包文件； 提供交易签名功能，签名后通过 witness\_node 向外广播； 通过 http rpc 的方式提供 API 供其他程序调用。

## 节点端口说明

启动DBXChain见证节点witness\_node

```bash
nohup witness_node --rpc-endpoint=127.0.0.1:38090 --p2p-endpoint=0.0.0.0:38091 >>witness.out 2>&1 &
```

端口种类及调用说明

| **端口类型** | **端口信息** |
| :---: | :---: |
| 38090 | witness\_node提供的rpc服务端口 |
| 38091 | P2P网络的通信接口，用于广播交易消息体和区块 |

命令行钱包cli\_wallet连接witness\_node:

```
cli_wallet -s ws://127.0.0.1:38090 -r 127.0.0.1:38091
```

端口种类及调用说明

| **端口类型** | **端口信息** |
| :---: | :---: |
| 38090 | 连接witness\_node提供的rpc服务端口 |
| 38091 | cli\_wallet提供的rpc服务端口 |




## **DBXChain节点介绍**

DBXChain节点主要包含witness\_node和cli\_wallet两部分。

witness\_node 通过 P2P 方式连接到DBXChain网络，从网络接收最新区块，向网络广播本地签署的交易包。

cli\_wallet 通过 websocket 方式连接到 witness\_node， 管理钱包文件； 提供交易签名功能，签名后通过 witness\_node 向外广播； 通过 http rpc 的方式提供 API 供其他程序调用。


### 启动见证节点

```bash
nohup witness_node --rpc-endpoint=127.0.0.1:38090 --p2p-endpoint=0.0.0.0:38091 2>&1 &
```

可使用--help 来查看命令参数  
witness\_node启动参数：

```
# 指定数据及配置文件存储的目录
--data-dir=trusted_node

# 指定rpc服务侦听地址及端口(端口可修改)，127.0.0.1限定本地访问rpc服务，若不限定本地访问，可指定0.0.0.0
--rpc-endpoint=127.0.0.1:38090

# 用于连接p2p网络，此参数不建议修改
--p2p-endpoint=0.0.0.0:38091 

# 内存中只跟踪指定帐户的交易历史，该选项可传入多次，跟踪多个帐户。请将1.2.2999 替换成你需要跟踪的账户数字 ID（在轻钱包账户页面里，账号头像下面会显示一个数字）
--track-account "\"1.2.2999\"" 

```

完全同步区块，大约需要30分钟以上。通过后台日志文件trusted\_node/logs/witness.log可查看区块同步进度，访问[DBXChain区块浏览器](https://block.dbx.io)查看最新区块。  
待区块同步至最新，DBXChain节点即部署成功。

