# witness_node 参数介绍

## 1. witness\_node操作 —— 启动链

### 1.1 创建和编辑初始文件

初始文件是用来定义区块链网络初始状态，如下：
* 修改初始文件中账户， 以及账户名和公钥
* 区块链资产和初次分发（包含核心资产）
* 私链参数的最初基准（包括费用）
* 初始见证人的账户签名秘钥


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

| 参数 | 说明 |
|:--- |:--- |
| -h [ --help ] | Print this help message and exit. |
| -d [ --data-dir ] arg |(="witness_node_data_dir") Directory containing databases,  configuration file, etc. |
| -v [ --version ] | Display version information |
| --create-genesis-json arg | Path to create a Genesis State at. If a well-formed JSON file exists at the path, it will be parsed and any missing fields in a Genesis State will be added, and any unknown fields will be removed. If no file or an invalid file is found, it will be replaced with an example Genesis State. |
| --replay-blockchain | Rebuild object graph by replaying all blocks |
| --resync-blockchain | Delete all blocks and re-sync with  network from scratch |
| --force-validate | Force validation of all transactions |
| --genesis-timestamp arg | Replace timestamp from genesis.json  with current time plus this many  seconds (experts only!) |
| --p2p-endpoint arg | Endpoint for P2P node to listen on |
| -s [ --seed-node ] arg | P2P nodes to connect to on startup (may specify multiple times) |
| --seed-nodes arg | JSON array of P2P nodes to connect to  on startup |
| -c [ --checkpoint ] arg | Pairs of [BLOCK_NUM,BLOCK_ID] that  should be enforced as checkpoints. |
| --rpc-endpoint [=arg(=127.0.0.1:8090)] | Endpoint for websocket RPC to listen on |
| --rpc-tls-endpoint [=arg(=127.0.0.1:8089)] | Endpoint for TLS websocket RPC to  listen on |
| -p [ --server-pem ] [=arg(=server.pem)] | The TLS certificate file for this  server |
| -P [ --server-pem-password ] arg | Password for this certificate |
| --genesis-json arg | File to read Genesis State from |
| --dbg-init-key arg | Block signing key to use for init  witnesses, overrides genesis file |
| --api-access arg | JSON file specifying API permissions |
| --plugins arg | Space-separated list of plugins to  activate |
| --io-threads [=arg(=0)] | Number of IO threads, default to 0 for  auto-configuration |

插件选项

| 参数 | 说明 |
|:--- |:--- |
| --enable-stale-production | Enable block production, even if the chain is stale. |
| --required-participation | Percent of witnesses (0-99) that must be participating in order to produce blocks |
| -w [ --witness-id ] arg | ID of witness controlled by this node (e.g. "1.6.5", quotes are required, may specify multiple times) |
| --private-key arg (=["DBX6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV","5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"]) | Tuple of [PublicKey, WIF private key] (may specify multiple times) |

debug_witness插件选项

| 参数 | 说明 |
|:--- |:--- |
| --debug-private-key arg (=["DBX6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV","5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"]) | Tuple of [PublicKey, WIF private key] (may specify multiple times) |

account_history插件选项

| 参数 | 说明 |
|:--- |:--- |
| --track-account arg | Account ID to track history for (may specify multiple times) |
| --partial-operations arg | Keep only those operations in memory that are related to account history tracking |
| --max-ops-per-account arg | Maximum number of operations per account will be kept in memory |

elasticsearch插件选项

| 参数 | 说明 |
|:--- |:--- |
| --elasticsearch-node-url arg | Elastic Search database node url |
| --elasticsearch-bulk-replay arg | Number of bulk documents to index on replay(5000) |
| --elasticsearch-bulk-sync arg | Number of bulk documents to index on a syncronied chain(10) |
| --elasticsearch-logs arg | Log bulk events to database |
| --elasticsearch-visitor arg | Use visitor to index additional  data(slows down the replay) |

market_history插件选项

| 参数 | 说明 |
|:--- |:--- |
| --bucket-size arg |(=[60,300,900,1800,3600,14400,86400]) Track market history by grouping orders into buckets of equal size measured in  seconds specified as a JSON array of  numbers |
| --history-per-size arg (=1000) | How far back in time to track history  for each bucket size, measured in the  number of buckets (default: 1000) |
| --max-order-his-records-per-market arg (=1000) Will only store this amount of matched  orders for each market in order history for querying, or those meet the other  option, which has more data (default:  1000) |
| --max-order-his-seconds-per-market arg (=259200) Will only store matched orders in last  X seconds for each market in order  history for querying, or those meet the other option, which has more data  (default: 259200 (3 days)) |

delayed_node插件选项

| 参数 | 说明 |
|:--- |:--- |
| --trusted-node arg | RPC endpoint of a trusted validating  node (required) |

snapshot插件选项，在指定的时间或者指定的出块号时创建快照。

| 参数 | 说明 |
|:--- |:--- |
| --snapshot-at-block arg | Block number after which to do a  snapshot |
| --snapshot-at-time arg | Block time (ISO format) after which to  do a snapshot |
| --snapshot-to arg | Pathname of JSON file where to store  the snapshot |

es_objects插件选项. 在es数据库中存储链对象

| 参数 | 说明 |
|:--- |:--- |
| --es-objects-elasticsearch-url arg | Elasticsearch node url |
| --es-objects-logs arg | Log bulk events to database |
| --es-objects-bulk-replay arg | Number of bulk documents to index on  replay(5000) |
| --es-objects-bulk-sync arg | Number of bulk documents to index on a  syncronied chain(10) |
| --es-objects-proposals arg | Store proposal objects |
| --es-objects-accounts arg | Store account objects |
| --es-objects-assets arg | Store asset objects |
| --es-objects-balances arg | Store balances objects |
| --es-objects-limit-orders arg | Store limit order objects |
| --es-objects-asset-bitasset arg | Store feed data |

grouped_orders插件选项

| 参数 | 说明 |
|:--- |:--- |
| --tracked-groups arg (=[10,100]) | Group orders by percentage increase on  price. Specify a JSON array of numbers  here, each number is a group, number 1  means 0.01%. |
