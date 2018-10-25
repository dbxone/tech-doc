# Private chain establishment

## 1. witness_node operation —— Start the chain

### 1.1 Create and edit the initial files

The initial files are used to define the initial status of the blockchain network, as follows：
* Modify the account, account name and public key in the initial files
* Blockchain asset and initial distribution（Including core asset）
* The initial standard of the private chain parameter（Including costs）
* The account signature encrypted key of the initial witness


Create an initial file named as `my-genesis.json`：

```
$ witness_node --create-genesis-json my-genesis.json
```

In the Graphene system, the only account included in the default initial block is `nathan`, all the witness, committee members and fund in the foundation block refer to the account. 


#### eg.1 Modify the private key of `nathan`

The default private key of `nathan` is:
> 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

Modify the private key by manually modifying the initial file.


#### eg.2 Modify the active witness updating time
```
"maintenance_interval": 600
```


### 1.2 Initialize the initial witness node, get the chain ID

The chain ID is the hash of the initial status. It is used to identify different chains.

```
witness_node --genesis-json my-genesis.json
```

**If the initial file is modified, the chain ID wil change, thus a different chain will be created.**

The following message means the completion of initialization, press `ctrl-c` to close the witness node:

```
3501235ms th_a main.cpp:165 main] Started witness node on a chain with 0 blocks.
3501235ms th_a main.cpp:166 main] Chain ID is 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

At this moment, the default data folder `witness_node_data_dir` is created, which can be designated by parameter `--data-dir <data_dir>`.

**`6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d` is the chain ID**

### 1.3 Set uo the witness

Edit `witness_node_data_dir/config.ini` to modify the configuration:

```
p2p-endpoint = 0.0.0.0:31010
seed-nodes = []
rpc-endpoint = 0.0.0.0:38090
genesis-json = my-genesis.json
enable-stale-production = true

# ID of witness controlled by this node (e.g. "1.6.5", quotes are required, may specify multiple times)
witness-id = "1.6.1"
witness-id = "1.6.2"
witness-id = "1.6.3"
witness-id = "1.6.4"
witness-id = "1.6.5"
witness-id = "1.6.6"
witness-id = "1.6.7"
witness-id = "1.6.8"
witness-id = "1.6.9"
witness-id = "1.6.10"
witness-id = "1.6.11"
```

The list above authorizes the witness node to generate blocks by its ID. Usually, every witness has different nodes, however we will initially stipulate that all witness will generate blocks at one node in the private chain. The private keys (used to sign the block) of those witness IDs have been provided in `config.ini`：

```
# Tuple of [PublicKey, WIF private key] (may specify multiple times)
private-key = ["DBX6MRyA...T5GDW5CV","5KQwrPb...tP79zkvFD3"]
```

The configuration option has the following meaning：

* `p2p-endpoint`  Designate the started p2p monitoring endpoint for other nodes to connenct, also serving as seed-node of other nodes.
* `rpc-endpoint`  Designate the started rpc monitoring endpoint for cli-wallet and web wallet to connect to witness.
* `genesis-json`  Set up the path of genesis.json, usually done at the moment the foundation block is generated when a new chain is created.
* `enable-stale-production` Let the node generate blocks no matter what the time of the blockchain data is. Usually this field is only set to be true at the moment the foundation block is generated when a new chain is created. When there are blocks already existed, do set the parameter to be false or leave it aside, otherwise the diversification can happen due to the incompleteness of data.
* `seed-nodes` Sets up the seed node set to connect to blockchain network quickly and synchronize blockchain data. It is set as empty at the moment the foundation block is generated when a new chain is created to prevent the default seed nodes from connecting to the official network (code). When connecting to the existed blockchain network, set up as many seed nodes as possible to speed up the sychronization.
* `witness-id`  Used to authorize the witness id representing the witness node to generate blocks, able to designate multiple ones. Usually one witness node authorizes one witness id, however the first node on the private chain designates 11 seed nodes.


### 1.4 Begin to generate blocks

```
witness_node
```

The blocks of the private chain will be generated in the following, you can see the following instruction:

```
********************************
*                              *
*   ------- NEW CHAIN ------   *
*   - Welcome to Graphene! -   *
*   ------------------------   *
*                              *
********************************
2322793ms th_a  main.cpp:176     main    ] Started witness node on a chain with 0 blocks.
2322794ms th_a  main.cpp:177     main    ] Chain ID is 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
2324613ms th_a  witness.cpp:185  block_production_loo ] Generated block #1 with timestamp 2016-01-21T22:38:40 at time 2016-01-21T22:38:40
2344604ms th_a  witness.cpp:185  block_production_loo ] Generated block #2 with timestamp 2016-01-21T22:39:00 at time 2016-01-21T22:39:00
2349616ms th_a  witness.cpp:185  block_production_loo ] Generated block #3 with timestamp 2016-01-21T22:39:05 at time 2016-01-21T22:39:05
2354605ms th_a  witness.cpp:185  block_production_loo ] Generated block #4 with timestamp 2016-01-21T22:39:10 at time 2016-01-21T22:39:10
```

If there is no log created by witness.log, it could be printed to the console, and you cna modify the `config.ini` file as follows，then restart witness.

```
[logger.default]
level=debug
appenders=stderr
```

## 2. cli_wallet operation

### 2.1 Establish new wallet

The wallet is used to save the private key of the account, here the name of the established wallet is `my-wallet.json`.
```
cli_wallet -w my-wallet.json -s ws://127.0.0.1:38090 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

When there is follwoing reminders, it means your client has matched the witness node successfully.
```
1987712ms th_a       main.cpp:136                  main                 ] key_to_wif( committee_private_key ): 5KCBDTcyDqzsqehcb52tW5nU6pXife6V2rX9Yf7c3saYSzbDZ5W 
1987713ms th_a       main.cpp:140                  main                 ] nathan_pub_key: DBX6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV 
1987713ms th_a       main.cpp:141                  main                 ] key_to_wif( nathan_private_key ): 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3 
Starting a new wallet with chain ID 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d (from CLI)
1987714ms th_a       main.cpp:188                  main                 ] wdata.ws_server: ws://127.0.0.1:38090 
1987717ms th_a       main.cpp:193                  main                 ] wdata.ws_user:  wdata.ws_password:  
Please use the set_password method to initialize a new wallet before continuing
new >>>
```


Before using your wallet, you have to set a password, which is `supersecret` here：

```
new >>> set_password supersecret
set_password supersecret
null
locked >>>
```

The wallet can be used only if it is unlocked. Unlock the wallet：

```
locked >>> unlock supersecret  
unlock supersecret
null
unlocked >>> 
```


### 2.2 Import nathan account

One wallet can store multiple accounts through commands.

To store an account to the wallet, you need to import the private key, for example, import `nathan` account as follows：

```
import_key nathan 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

### 2.3 Assign asset on the chain to nathan account


Assign the DBX which is set in the initial file as the asset on the chain to `nathan`：

```
import_balance nathan ["5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"] true
```

It is able to query the account balance now：


```
list_account_balances nathan
```

### 2.4 Upgrade nathan to lifelong member\(LTM\)

Lifelong members have some franchise which is not available to common members:

1. Able to create premium account name
2. 80% transaction payment fee back
3. 80% of the transaction payment fee by the recommended account will be returned to the referenece
4. Able to create witness

Here upgrade `nathan` to a lifelong member.

```
upgrade_account nathan true
```

Restart the client, otherwise it can't determine whether `nathan` has successfully upgraded. Terminate the client by `ctrl-c`.

```
cli_wallet -w my-wallet.json -s ws://127.0.0.1:38090 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

Find the account property
```
get_account nathan
```

Property value of `membership_expiration_date` is `1969-12-31T23:59:59`，meaning upgrading successfully.


### 2.5 Register new account alpha

After upgrading successfully, we can register new accounts through `nathan`，but we need to have the public and private keys of the new account.

Generate encrypted key pairs：

```
suggest_brain_key
```

Register new account alpha

```
register_account alpha DBX6vQtDEgHSickqe9itW8fbFyUrKZK5xsg4FRHzQZ7hStaWqEKhZ DBX6vQtDEgHSickqe9itW8fbFyUrKZK5xsg4FRHzQZ7hStaWqEKhZ nathan nathan 0 true
```


### 2.6 nathan transfer to alpha

```
transfer nathan alpha 1 DBX "" true
```

Query nathan balance：

```
list_account_balances alpha
```

Private chain has been successfully established！
