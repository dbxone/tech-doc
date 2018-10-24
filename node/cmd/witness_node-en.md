# witness_node Initiating parameter


| Parameter | Explanation |
|:--- |:--- |
| -h [ --help ] | Print this help message and exit. <br> Help message |
| -d [ --data-dir ] arg (="witness_node_data_dir") | Directory containing databases, configuration file, etc. <br> Designate the directory for the storage of data and configuration file |
| -v [ --version ] | Display version information <br> Version information |
| --create-genesis-json arg | Path to create a Genesis State at. If a well-formed JSON file exists at the path, it will be parsed and any missing fields in a Genesis State will be added, and any unknown fields will be removed. If no file or an invalid file is found, it will be replaced with an example Genesis State. <br> Establish the initial file. If the file has already existed, it will be parsed and missing configuration option will be added meanwhile delete the unidentifiable type.|
| --replay-blockchain | Rebuild object graph by replaying all blocks <br> Replay all the downloaded blocks and rebuild the index, time consuming |
| --resync-blockchain | Delete all blocks and re-sync with  network from scratch <br> Delete all the downloaded data, resynchronize blocks |
| --force-validate | Force validation of all transactions |
| --genesis-timestamp arg | Replace timestamp from genesis.json  with current time plus this many  seconds (experts only!) |
| --p2p-endpoint arg | Endpoint for P2P node to listen on <br> Used to the p2p linking service between nodes |
| -s [ --seed-node ] arg | P2P nodes to connect to on startup (may specify multiple times) |
| --seed-nodes arg | JSON array of P2P nodes to connect to  on startup |
| -c [ --checkpoint ] arg | Pairs of [BLOCK_NUM,BLOCK_ID] that  should be enforced as checkpoints. |
| --rpc-endpoint [=arg(=127.0.0.1:8090)] | Endpoint for websocket RPC to listen on <br> Designate rpc serive monitoring address and endpoint (the endpoint could be modified)，127.0.0.1 only allows local visiting access to rpc service，otherwise you could designate 0.0.0.0 |
| --rpc-tls-endpoint [=arg(=127.0.0.1:8089)] | Endpoint for TLS websocket RPC to  listen on |
| -p [ --server-pem ] [=arg(=server.pem)] | The TLS certificate file for this  server |
| -P [ --server-pem-password ] arg | Password for this certificate |
| --genesis-json arg | File to read Genesis State from |
| --dbg-init-key arg | Block signing key to use for init  witnesses, overrides genesis file |
| --api-access arg | JSON file specifying API permissions |
| --plugins arg | Space-separated list of plugins to  activate |
| --io-threads [=arg(=0)] | Number of IO threads, default to 0 for  auto-configuration |

Plug-in option

| Parameter | Explanation |
|:--- |:--- |
| --enable-stale-production | Enable block production, even if the chain is stale. |
| --required-participation | Percent of witnesses (0-99) that must be participating in order to produce blocks |
| -w [ --witness-id ] arg | ID of witness controlled by this node (e.g. "1.6.5", quotes are required, may specify multiple times) |
| --private-key arg <br> (=["DBX6MR...W5CV","5KQwrP...vFD3"]) | Tuple of [PublicKey, WIF private key] (may specify multiple times) |

debug_witness plug-in option

| Parameter | Explanation |
|:--- |:--- |
| --debug-private-key arg <br> (=["DBX6MR...W5CV","5KQwrP...vFD3"]) | Tuple of [PublicKey, WIF private key] (may specify multiple times) |

account_history plug-in option

| Parameter | Explanation |
|:--- |:--- |
| --track-account arg | Account ID to track history for (may specify multiple times) <br> Only transaction history of desiganted account will be tracked in RAM, such option could be imported for multiple times to track multiple accounts. Please substitute 1.2.2999 to the number ID of the account you need to track（In the light weighted wallet account page, there will be a number under the account photo）|
| --partial-operations arg | Keep only those operations in memory that are related to account history tracking <br> 和--track-account / --max-ops-per-account Mixed options, able to save more RAM, this parameter is recommended |
| --max-ops-per-account arg | Maximum number of operations per account will be kept in memory <br> Each account can reserve "NUM" transaction records in RAM at most, whole is the default |

elasticsearch plug-in option

| Parameter | Explanation |
|:--- |:--- |
| --elasticsearch-node-url arg | Elastic Search database node url |
| --elasticsearch-bulk-replay arg | Number of bulk documents to index on replay(5000) |
| --elasticsearch-bulk-sync arg | Number of bulk documents to index on a syncronied chain(10) |
| --elasticsearch-logs arg | Log bulk events to database |
| --elasticsearch-visitor arg | Use visitor to index additional  data(slows down the replay) |

market_history plug-in option

| Parameter | Explanation |
|:--- |:--- |
| --bucket-size arg |(=[60,300,900,1800,3600,14400,86400]) Track market history by grouping orders into buckets of equal size measured in  seconds specified as a JSON array of  numbers |
| --history-per-size arg (=1000) | How far back in time to track history  for each bucket size, measured in the  number of buckets (default: 1000) |
| --max-order-his-records-per-market arg (=1000) | Will only store this amount of matched  orders for each market in order history for querying, or those meet the other  option, which has more data (default:  1000) |
| --max-order-his-seconds-per-market arg (=259200) | Will only store matched orders in last  X seconds for each market in order  history for querying, or those meet the other option, which has more data  (default: 259200 (3 days)) |

delayed_node plug-in option

| Parameter | Explanation |
|:--- |:--- |
| --trusted-node arg | RPC endpoint of a trusted validating  node (required) |

snapshot plug-in option, create snapshot at designated time or designated block number.

| Parameter | Explanation |
|:--- |:--- |
| --snapshot-at-block arg | Block number after which to do a  snapshot |
| --snapshot-at-time arg | Block time (ISO format) after which to  do a snapshot |
| --snapshot-to arg | Pathname of JSON file where to store  the snapshot |

es_objects plug-in option. Store chain objectives in es database

| Parameter | Explanation |
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

grouped_orders plug-in option

| Parameter | Explanation |
|:--- |:--- |
| --tracked-groups arg (=[10,100]) | Group orders by percentage increase on  price. Specify a JSON array of numbers  here, each number is a group, number 1  means 0.01%. |


# Exit witness_node

* If witness_node is not running at the back desk, execute Ctrl + C once, waiting for the program to quit automatically after saving RAM data.

* If witness_node is running at the back desk, execute `kill -s SIGINT $(pgrep witness_node)`, waiting for the program to quit automatically after saving RAM data. Do not use kill -9, otherwise it will rebuild the index when you start next time so that it will be slow.

* If abnormal exit happens, it has great possiblity to rebuild the index when you restart and it will be slow. If witness_node is abnormal, normally you can try to restart with --replay-blockchain parameter, namely to rebuild the index manually.


# Block synchronization error

Observe back desk log file trusted_node/logs/witness.log. If the log keeps reporting error such as "unlinkable block", "block does not link to known chain"，there will be block synchronization error.

Solutions：

* Abnormal block synchronization, it might be due to the local blockchain files are broken. It needs to terminate witness_node program，then delete trusted_node, restart witness_node.

* Or do not delete trusted_node directory，initiate command with parameter --resync-blockchain，then it will resynchronize blocks.
