# 智能合约的编译、部署、运行

## 1. 编译合约

使用dxx的模板创建一个helloworld合约:

```
dxx -n helloworld
```

## 2. 编译合约，生成wast和abi

编译合约，生成wast和abi文件:

```
dxx -o helloworld/helloworld.wast helloworld/helloworld.cpp
dxx -g helloworld/helloworld.abi helloworld/helloworld.cpp
```

## 3. 部署合约

### 3.1 打开钱包，连接链节点。

```
cli_wallet -s ws://ip:port --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

解锁钱包
```
locked >>> unlock mylocalpassword
```

### 3.2 导入钱包私钥

```
unlocked >>> import_key your_account_name your_private_key
```

部署合约helloworld

```
unlocked >>> deploy_contract helloworld your_account_name 0 0 ./helloworld DBX true
```
| 参数 | 解释 |
| :--- | :--- |
| your_accoutn_name | 部署合约的账户 |
| 0 | 虚拟机类型 |
| 0 | 虚拟机版本 |
| ./helloworld | 为wast/abi文件所在路径 |
| DBX | 手续费资产类型 |
| true | 发起广播 |
 
 
 
 
 
 

#### 5. 调用合约
部署合约成功后，可以使用call_contract接口查询合约

```
unlocked >>> call_contract nathan helloworld null hi "{\"user\":\"abcdefg\"}" DBX true

```
