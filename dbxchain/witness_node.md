# witness_node 参数介绍


| 参数 | 说明 |
|:--- |:--- |
| -h [ --help ] | Print this help message and exit. <br> 帮助信息 |
| -d [ --data-dir ] arg (="witness_node_data_dir") | Directory containing databases, configuration file, etc. <br> 指定数据及配置文件存储的目录 |
| -v [ --version ] | Display version information <br> 版本信息 |
| --create-genesis-json arg | Path to create a Genesis State at. If a well-formed JSON file exists at the path, it will be parsed and any missing fields in a Genesis State will be added, and any unknown fields will be removed. If no file or an invalid file is found, it will be replaced with an example Genesis State. <br> 创建初始文件，如果文件已经存在，将对此文件进行解析，添加上不存在配置选项，同时删除不识别的选型。|
| --replay-blockchain | Rebuild object graph by replaying all blocks <br> 重放所有已下载的区块并重建索引，比较耗时 |
| --resync-blockchain | Delete all blocks and re-sync with  network from scratch <br> 删除所有已下载数据，重新同步区块 |
| --force-validate | Force validation of all transactions |
| --genesis-timestamp arg | Replace timestamp from genesis.json  with current time plus this many  seconds (experts only!) |
| --p2p-endpoint arg | Endpoint for P2P node to listen on <br> 用于节点之间的p2p链接服务 |
| -s [ --seed-node ] arg | P2P nodes to connect to on startup (may specify multiple times) |
| --seed-nodes arg | JSON array of P2P nodes to connect to  on startup |
| -c [ --checkpoint ] arg | Pairs of [BLOCK_NUM,BLOCK_ID] that  should be enforced as checkpoints. |
| --rpc-endpoint [=arg(=127.0.0.1:8090)] | Endpoint for websocket RPC to listen on <br> 指定rpc服务侦听地址及端口(端口可修改)，127.0.0.1限定本地访问rpc服务，若不限定本地访问，可指定0.0.0.0 |
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
| --private-key arg <br> (=["DBX6MR...W5CV","5KQwrP...vFD3"]) | Tuple of [PublicKey, WIF private key] (may specify multiple times) |

debug_witness插件选项

| 参数 | 说明 |
|:--- |:--- |
| --debug-private-key arg <br> (=["DBX6MR...W5CV","5KQwrP...vFD3"]) | Tuple of [PublicKey, WIF private key] (may specify multiple times) |

account_history插件选项

| 参数 | 说明 |
|:--- |:--- |
| --track-account arg | Account ID to track history for (may specify multiple times) <br> 内存中只跟踪指定帐户的交易历史，该选项可传入多次，跟踪多个帐户。请将1.2.2999 替换成你需要跟踪的账户数字 ID（在轻钱包账户页面里，账号头像下面会显示一个数字）|
| --partial-operations arg | Keep only those operations in memory that are related to account history tracking <br> 和--track-account / --max-ops-per-account 选项结合，可以进一步节省内存，建议带上此参数 |
| --max-ops-per-account arg | Maximum number of operations per account will be kept in memory <br> 每个账户在内存中最多保存NUM条交易记录，默认是全部 |

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
| --max-order-his-records-per-market arg (=1000) | Will only store this amount of matched  orders for each market in order history for querying, or those meet the other  option, which has more data (default:  1000) |
| --max-order-his-seconds-per-market arg (=259200) | Will only store matched orders in last  X seconds for each market in order  history for querying, or those meet the other option, which has more data  (default: 259200 (3 days)) |

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
