
#  智能合约快速入门

------------
## 1. 智能合约介绍

DBXChain智能合约2.0，底层使用WebAssembly虚拟机，目前支持C++语言的智能合约编写。
开发者使用C++编写智能合约，通过llvm将代码编译成WebAssembly（又名WASM），部署到区块链上，通过智能合约ABI(Application Binary Interface，应用程序的二进制接口)和智能合约交互。

### 1.1 合约帐户设计
  1. 帐户分2种：普通帐户和合约帐户
  2. 合约帐户，由普通帐户通过部署合约的方式创建，合约帐户无私钥，资产权限由合约代码控制
  3. 合约帐户对象，code字段存储合约代码, abi存储合约代码和abi
  4. 合约代码不支持更新

### 1.2 合约的持久化存储
  1. 定义合约的数据存储格式； 定义线性存储空间，每个元素是一个struct类型
  2. witness_node运行时，合约的持久化存储，放内存；程序退出时，写入磁盘；后期可以考虑优化内存(磁盘+缓存)。
  3. 封装读写持久化存储的API，  提供读、写、检索方法的接口供合约调用
  4. 合约只能写自己的存储空间，可以读其它合约的存储空间，但不可直接写；  同一合约内不同帐户的存储空间，由用户合约代码控制权限
  5. 合约内可以根据区块号获取区块，读取外部状态

### 1.3 智能合约公共库，供智能合约在虚拟机内部调用
 1. 提供API，获取head block num,  获取head block id
 2. get_balance 获取外部帐户余额
 3. 加解密API、验签API
 4. 持久化存储API

### 1.4 销毁合约(暂不支持)
合约内可以提供销毁方法，如：
selfdestruct(string account) 将资产转至recipient帐户，然后销毁合约
回收的存储空间，按全局手续费参数计算，奖励给合约创建者(从系统资金池中获取,  最多返还存储价格的20%)。

### 1.5 合约调用合约(暂不支持)
目前只能由普通帐户和合约帐户交互，不支持合约间交互。


## 2. 快速开始

可以本地编译搭建DBXChain私链，通过命令行方式编译、部署、调用智能合约。

### 2.1 [编译DBXChain链](compile.md)

### 2.2 [搭建私链](../dbxchain/private-chain.md)

### 2.3 [编译部署运行合约](contract-run.md)


## 3. 智能合约示例

* [helloworld合约](examples/helloworld.md)
* [充值提现合约](examples/bank.md)
* [红包合约](examples/redpacket.md)
* [线性释放资产合约](examples/linear_vesting_asset.md)
* [基于hash验证的猜谜合约](examples/riddle.md)


## 4. 智能合约 API 参考文档
* [api参考文档](contract-api.md)
* [存储参考文档](contract-storage_usage.md)



### 其它参考：
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

testnet 安装文档 ：https://github.com/dbxone/tech-doc/blob/contract/test%20net.md

testnet 区块浏览器：https://testnet.explorer.dbxchain.org/#/

testnet 网页钱包：https://testnet.wallet.dbxchain.org/

testnet 钱包接入点：wss://testnet.dbxchain.org

[note] 测试智能合约时需要注意：

* 目前的存储表(Multi-Index table)不支持的类型：int128, int256, float, double。
