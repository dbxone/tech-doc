
# 测试网络

DBXChain官方测试网络访问节点：13.57.136.245

## 1. 测试网络配置

下载全节点配置文件：
```
wget http://13.57.136.245/my-genesis.json
wget http://13.57.136.245/config.ini
```

vim config.ini
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

... ...
```


## 2. 钱包服务

```
cli_wallet -w wallet.json -s ws://0.0.0.0:38090 -r 0.0.0.0:38091 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

## 3. 水龙头服务

水龙头配置

`vim config/faucet.yml`

```
cli_wallet_connection: ws://127.0.0.1:38091
registrar_account: nathan
referrer_percent: 50
refcode_prefix: F01

default_url: 0.0.0.0
default_port: 3000
... ...
```

## 4. web钱包

web钱包地址 : http://13.57.136.245:18080

## 5. 轻钱包

轻钱包连接方式 : 

```
cli_wallet -w wallet.json -s ws://13.57.136.245:38090 -r 127.0.0.1:38091 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

具体参数使用请查阅[cli_wallet使用](../node/cmd/cli_wallet.md)
