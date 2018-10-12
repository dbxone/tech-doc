# 私有链搭建

##1. witness\_node操作 —— 启动链

###1.1 创建和编辑初始文件

初始文件是用来定义区块链网络初始状态，如下：
* 修改初始文件中账户， 以及账户名和公钥
* 区块链资产和初次分发（包含核心资产）
* 私链参数的最初基准（包括费用）
* 初始见证人的账户签名秘钥


创建一个名为`my-genesis.json`的初始文件：

```
$ witness_node --create-genesis-json my-genesis.json
```

石墨烯系统中默认的初始化块中包含唯一一个账户`nathan`，创世区块中的所有见证人、理事会成员和基金会都是改账户。 


#### eg.1 修改`nathan`私钥

`nathan`的默认私钥为:
> 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

通过手动修改初始文件对私钥进行修改。


#### eg.2 修改活跃见证人更新时间
```
"maintenance_interval": 600
```


###1.2 初始化证人节点，获取链ID

链ID是初始状态的哈希值。它用来区分不同的链。

```
witness_node --genesis-json my-genesis.json
```

**如修改了初始文件，链ID将会变化，因此会创建出一条不同的链。**

出现如下信息，代表初始化已经完成，按`ctrl-c` 关闭见证人节点:

```
3501235ms th_a main.cpp:165 main] Started witness node on a chain with 0 blocks.
3501235ms th_a main.cpp:166 main] Chain ID is 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

此时，默认数据文件夹`witness_node_data_dir`被创建，可以通过参数`--data-dir <data_dir>`来指定默认数据文件夹。

**`6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d` 即为链ID。**

###1.3 配置见证人

编辑`witness_node_data_dir/config.ini`修改配置：

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

上述列表授权了见证人节点用见证人ID来生成区块. 正常情况下，每个见证人的节点不同，但在私有链中，我们会先设定成全体见证人在同一个节点生产区块。这些见证人ID的私钥（用来签署区块）已经在`config.ini`中提供：

```
# Tuple of [PublicKey, WIF private key] (may specify multiple times)
private-key = ["DBX6MRyA...T5GDW5CV","5KQwrPb...tP79zkvFD3"]
```

初始文件是用来定义区块链网络初始状态，如下：

* `p2p-endpoint`  指定开启的p2p监听端口，以方便其他节点连接，可以作为其他节点的seed-node 。
* `rpc-endpoint`  指定开启的rpc监听端口，以方便cli-wallet 和web 钱包与证人节点连接。
* `genesis-json`  设置genesis.json 的路径，通常只在创建新链生产创世区块时设置。
* `enable-stale-production`  让本节点无视区块链数据的时间，无论如何都生成区块数据。该字段通常只在创建新链生产创世区块时设为true。当已存在区块链时，一定要将本参数设为false或者不管，否则会因数据不完整导致分叉。
* `seed-nodes`  设置种子节点集合，以方便快速连接到区块链网络和同步区块链数据。在创建新链生产创世区块时设为空，以防止连接到正式网络（代码）中的默认种子节
点。当连接已有区块链网络时，尽可能多的设置种子节点以加快同步速度。
* `witness-id`  用于授权本证人节点所代表的证人id产生区块，可指定多个。一般来说一个证人节点授权一个证人id，私链第一个节点指定了11个。


###1.4 开始生产区块

```
witness_node
```

之后私链的区块将开始生成，你会看到如下指示:

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

如果witness.log无日志生成，可以将日志打印打控制台，可以修改`config.ini`文件如下，然后重新启动witness

```
[logger.default]
level=debug
appenders=stderr
```

##2. cli_wallet操作

###2.1 创建新钱包

钱包用来保存账户的私钥，此处创建的钱包名称为`my-wallet.json`。
```
cli_wallet -w my-wallet.json -s ws://127.0.0.1:38090 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

如下提示，意味着你的客户端已经成功匹配见证人节点。
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


使用钱包钱，需要为钱包设置密码，此处为`supersecret`：

```
new >>> set_password supersecret
set_password supersecret
null
locked >>>
```

钱包解锁后，才能使用。解锁钱包：

```
locked >>> unlock supersecret  
unlock supersecret
null
unlocked >>> 
```


###2.2 导入nathan账户

一个钱包通过命令可以保存多个账户。

账户保存进钱包需要导入私钥，以下导入`nathan`账户：

```
import_key nathan 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

###2.3 将链上资产赋给nathan账户


将`config.ini`中设置链上资产DBX赋给`nathan`：

```
import_balance nathan ["5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"] true
```

此时可查看账户余额：


```
list_account_balances nathan
```

###2.4 升级nathan为终身会员\(LTM\)

终身会员拥有普通会员不具备的一些权限，比如通常我们用一个已有账户来创建新账户，只有成为终身会员才能注册其他账户，此处升级`nathan`为终身会员。

```
upgrade_account nathan true
```

重启客户端，否则将无法识别`nathan`已经成功升级。通过`ctrl-c`停止客户端。

```
cli_wallet -w my-wallet.json -s ws://127.0.0.1:38090 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

查看账户属性
```
get_account nathan
```

`membership_expiration_date`的属性值应该是`1969-12-31T23:59:59`，代表成功升级。


###2.5 注册新账户alpha

成功升级后，我们可以通过`nathan`来注册新账户，但首先我们需要拥有新账户的公私钥。

生成公私钥对：

```
suggest_brain_key
```

注册新账户alpha

```
register_account alpha DBX6vQtDEgHSickqe9itW8fbFyUrKZK5xsg4FRHzQZ7hStaWqEKhZ DBX6vQtDEgHSickqe9itW8fbFyUrKZK5xsg4FRHzQZ7hStaWqEKhZ nathan nathan 0 true
```


###2.6 nathan转账给alpha

```
transfer nathan alpha 1 DBX "" true
```

查看nathan余额：

```
list_account_balances alpha
```

