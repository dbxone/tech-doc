# 测试网络简介

测试网络是DBXChain的外部测试环境，参数与主链相同，开发者可以利用测试网络部署节点、申请见证人或对底层作出其他升级。

## 测试网络部署方法

测试网络种子节点：testnet.dbxchain.org:38091 目前只有一个节点，社区开发者贡献节点可以加入测试网络，申请见证人。

钱包接入点：`wss://testnet.dbxchain.org`

**访问[testnet网页钱包](https://testnet.wallet.dbxchain.org/#/)  ```https://testnet.wallet.dbxchain.org/#/``` 注册钱包帐户。
注册完成后，点击[这里](http://blockcity.mikecrm.com/2SVDb67) 申领测试DBX。**

### 1. 下载程序, 解压

**首先请**[**点击这里**](https://github.com/dbxone/dbxchain/releases/latest)**下载最新程序, 解压**

```js
wget http://dbx-package.oss-cn-hangzhou.aliyuncs.com/dbxchain/dbx_ubuntu_1.0.180809.beta.tar.gz -O dbx_ubuntu_1.0.180809.beta.tar.gz
# 解压程序
tar zxvf dbx_ubuntu_1.0.180809.beta.tar.gz
```

### 2. 下载testnet的genesis.json文件

```
wget http://dbx-package.oss-cn-hangzhou.aliyuncs.com/dbxchain/genesis/testnet-genesis.json -O genesis.json
```

### 3. 启动witness\_node，同步区块

```
./programs/witness_node/witness_node --data-dir=testnet_node --rpc-endpoint="0.0.0.0:38090" --p2p-endpoint="0.0.0.0:9999" --seed-nodes='["testnet.dbxchain.org:38091"]' --genesis-json genesis.json &
```

目前测试网络数据量不大，可以跑全节点。通过后台日志文件testnet\_node/logs/witness.log可查看区块同步进度。 
区块同步完成后，可以运行命令行钱包cli\_wallet。

### 4. 运行命令行钱包cli\_wallet

```
./programs/cli_wallet/cli_wallet -sws://127.0.0.1:38090  -r 127.0.0.1:38091 --data-dir=testnet_node --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```



