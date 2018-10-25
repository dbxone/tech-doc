# Testnet

DBXChain official testnet accessing node：13.57.136.245

## 1. Testnet configuration

Download the configuration files of full nodes：
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


## 2. Wallet service

```
cli_wallet -w wallet.json -s ws://0.0.0.0:38090 -r 0.0.0.0:38091 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

## 3. Faucet service

Faucet configuration

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

## 4. web wallet

web wallet address: http://13.57.136.245:18080

## 5. Light weighted wallet

Light weighted wallet connecting approach : 

```
cli_wallet -w wallet.json -s ws://13.57.136.245:38090 -r 127.0.0.1:38091 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

Please refer to [cli_wallet usage](../node/cmd/cli_wallet.md) for the detailed parameter usage.
