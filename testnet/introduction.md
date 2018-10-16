
## 其它参考：
#### 安装DBXChain testnet网络全节点程序
如果不想使用testnet提供的接入点，也可以本地部署一个全节点。
安装DBXChain testnet全节点安装方法：

```
# 下载testnet的genesis.json文件
wget http://dbx-package.oss-cn-hangzhou.aliyuncs.com/dbxchain/genesis/testnet-genesis.json -O genesis.json

# 下载程序包， ubuntu安装包
wget http://dbx-package.oss-cn-hangzhou.aliyuncs.com/dbxchain/dbx_ubuntu_1.0.180809.beta.tar.gz -O dbx_ubuntu_1.0.180809.beta.tar.gz
# 解压
tar zxvf dbx_ubuntu_1.0.180809.beta.tar.gz

# 启动witness_node, 同步testnet区块数据
./programs/witness_node/witness_node --data-dir=testnet_node --rpc-endpoint="0.0.0.0:38090" --p2p-endpoint="0.0.0.0:9999" --seed-nodes='["testnet.dbxchain.org:38091"]' --genesis-json genesis.json &

# 启动完成后，可以观察./testnet_node/log/witness.log观察区块同步情况，区块同步过程中每10000个区块会打印一条日志，同步完成后，每3秒打印一条日志ß
```

testnet 安装文档 ：https://github.com/dbxone/tech-doc/blob/master/testnet.md

testnet 区块浏览器：https://testnet.explorer.dbxchain.org/#/

testnet 网页钱包：https://testnet.wallet.dbxchain.org/

testnet 钱包接入点：wss://testnet.dbxchain.org

[note] 测试智能合约时需要注意：

* 目前的存储表(Multi-Index table)不支持的类型：int128, int256, float, double。
