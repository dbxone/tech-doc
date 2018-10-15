# 第一个智能合约程序 helloworld

## 1. [源代码](https://github.com/dbxone/dbxchain/blob/contract/contracts/examples/helloworld/helloworld.cpp)

helloworld的源代码也可以用dxx模板进行生成:

```
dxx -n helloworld
```

代码如下:
```
#include <graphenelib/contract.hpp>
#include <graphenelib/dispatcher.hpp>
#include <graphenelib/print.hpp>
#include <graphenelib/types.h>

using namespace graphene;

class helloworld : public contract
{
  public:
    helloworld(uint64_t id)
        : contract(id)
    {
    }

    /// @abi action
    void hi(std::string user)
    {
        print("hi, ", user, "\n");
    }
};

GRAPHENE_ABI(helloworld, (hi))
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
| your_account_name | 部署合约的账户 |
| 0 | 虚拟机类型 |
| 0 | 虚拟机版本 |
| ./helloworld | 为wast/abi文件所在路径 |
| DBX | 手续费资产类型 |
| true | 发起广播 |
 
## 4. 调用合约

```
unlocked >>> call_contract your_account_name helloworld null hi "{\"user\":\"abcdefg\"}" DBX true

```
| 参数 | 解释 |
| :--- | :--- |
| your_account_name | 调用合约的账户 |
| helloworld | 调用的哪个合约 |
| null | 设置调用合约的手续费 |
| hi | 调用合约的哪个方法 |
| "{\"user\":\"abcdefg\"} | 调用的合约方法的参数 |
| DBX | 手续费资产类型 |
| true | 发起广播 |


## 5. 结果

在witness_node运行日志中可以查看到如下运行信息:

```
[(20,hi)->20] CONSOLE OUTPUT BEGIN =====================
hi, abcdefg

[(20,hi)->20] CONSOLE OUTPUT END =====================
```

此处helloworld的智能合约id是20.