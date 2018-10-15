# API测试例子

## 1. [源代码](https://github.com/dbxone/dbxchain/blob/contract/contracts/examples/apitest/apitest.cpp)


代码如下:
```
#include <graphenelib/contract.hpp>
#include <graphenelib/dispatcher.hpp>
#include <graphenelib/print.hpp>
#include <graphenelib/types.h>
#include <graphenelib/action.h>
#include <graphenelib/global.h>
#include <graphenelib/asset.h>

using namespace graphene;

class apitest : public contract
{
	public:
		apitest(uint64_t id)
			: contract(id)
		{
		}

		void show(std::string account_to, std::string asset, uint64_t amount)
		{
			print("get_head_block_num=", get_head_block_num(), "\n");
			print("get_head_block_time=", get_head_block_time(), "\n");
			print("get_trx_sender=", get_trx_sender(), "\n");

			print("current_receiver=", current_receiver(), "\n");
			print("get_action_asset_id=", get_action_asset_id(), "\n");
			print("get_action_asset_amount=", get_action_asset_amount(), "\n");
			print("get_balance=", get_balance(current_receiver(), get_action_asset_id()), "\n");

			print("account_to=", account_to, ", id=", get_account_id(account_to.c_str(),account_to.length()), "\n");
			print("asset=", asset, ", id=", get_asset_id(asset.c_str(), asset.length()), "\n");
			print("amount=", amount, "\n");
		}

		/// @abi action
		void transfer(std::string account_to, std::string asset, uint64_t amount)
		{
			printf("------- start withdraw_asset -----\n");
			withdraw_asset(current_receiver(), get_account_id(account_to.c_str(),account_to.length()),  get_asset_id(asset.c_str(), asset.length()), amount);
		}
};

GRAPHENE_ABI(apitest, (transfer)(show))
```

## 2. 编译合约，生成wast和abi

编译合约，生成wast和abi文件:

```
dxx -o apitest/apitest.wast apitest/apitest.cpp
dxx -g apitest/apitest.abi apitest/apitest.cpp
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

部署合约helloworld

```
unlocked >>> deploy_contract apitest nathan 0 0 ./apitest DBX true
```
| 参数 | 解释 |
| :--- | :--- |
| nathan | 部署合约的账户 |
| 0 | 虚拟机类型 |
| 0 | 虚拟机版本 |
| ./apitest | 为wast/abi文件所在路径 |
| DBX | 手续费资产类型 |
| true | 发起广播 |
 
## 4. 调用合约

### 查看api相关调用结果

```
unlocked >>> call_contract nathan apitest null show "{\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" DBX true

```
| 参数 | 解释 |
| :--- | :--- |
| nathan | 调用合约的账户 |
| apitest | 调用的哪个合约 |
| null | 设置调用合约的手续费 |
| show | 调用合约的哪个方法 |
| {\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" | 调用的合约方法的参数 |
| DBX | 手续费资产类型 |
| true | 发起广播 |

### 调用转账接口

```
unlocked >>> call_contract nathan apitest null transfer "{\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" DBX true

```
| 参数 | 解释 |
| :--- | :--- |
| nathan | 调用合约的账户 |
| apitest | 调用的哪个合约 |
| null | 设置调用合约的手续费 |
| transfer | 调用合约的哪个方法 |
| {\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" | 调用的合约方法的参数 |
| DBX | 手续费资产类型 |
| true | 发起广播 |

查看transfer账户相关内容
```
list_account_balances nathan
get_account_history nathan 100
```
可以看到nathan给alpha转了50个DBX的日历。