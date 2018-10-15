# 这个合约用来调用helloworld的hi方法

## 1. [源代码](https://github.com/dbxone/dbxchain/blob/contract/contracts/examples/call-helloworld/call-helloworld.cpp)

代码如下:
```
#include <graphenelib/action.h>
#include <graphenelib/action.hpp>
#include <graphenelib/contract.hpp>
#include <graphenelib/dispatcher.hpp>
#include <graphenelib/print.hpp>

using namespace graphene;

class call_helloworld : public contract
{
  public:
    call_helloworld(uint64_t uname)
        : contract(uname)
    {
    }

    /// @abi action
    void call_hi(uint64_t act_id)
    {
        print("call helloworld->hi ", act_id);
        std::string s = "abc";
        action a(act_id, N(hi), bytes(s.begin(), s.end()));
        a.send();
    }
};

GRAPHENE_ABI(call_helloworld, (call_hi))

```

## 2. 编译合约，生成wast和abi

编译合约，生成wast和abi文件:

```
dxx -o call-helloworld/call-helloworld.wast call-helloworld/call-helloworld.cpp
dxx -g call-helloworld/call-helloworld.abi call-helloworld/call-helloworld.cpp
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
unlocked >>> import_key nathan your_private_key
```

部署合约

```
unlocked >>> deploy_contract call-helloworld nathan 0 0 ./call-helloworld DBX true
```
| 参数 | 解释 |
| :--- | :--- |
| nathan | 部署合约的账户 |
| 0 | 虚拟机类型 |
| 0 | 虚拟机版本 |
| ./call-helloworld | 为wast/abi文件所在路径 |
| DBX | 手续费资产类型 |
| true | 发起广播 |
 
## 4. 调用合约

```
unlocked >>> call_contract nathan call-helloworld null call_hi "{\"act_id\":20}" DBX true

```
| 参数 | 解释 |
| :--- | :--- |
| nathan | 调用合约的账户 |
| call-helloworld | 调用的哪个合约 |
| null | 设置调用合约的手续费 |
| call_hi | 调用合约的哪个方法 |
| "{\"act_id\":20}" | 调用的合约方法的参数 |
| DBX | 手续费资产类型 |
| true | 发起广播 |


## 5. 结果

在witness_node运行日志中可以查看到如下运行信息:

```
[(21,call_hi)->21] CONSOLE OUTPUT BEGIN =====================
hi contract:20

[(21,call_hi)->21] CONSOLE OUTPUT END =====================

... ...

[(20,hi)->20] CONSOLE OUTPUT BEGIN =====================
hi

[(20,hi)->20] CONSOLE OUTPUT END =====================
```

可以看到helloworld的hi方法被调用。