# API testing case

## 1. [Source code](https://github.com/dbxone/dbxchain/blob/contract/contracts/examples/apitest/apitest.cpp)


The code is shown as follows:
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

## 2. Complie the contract, generate wast and abi

Complie the contract, generate wast and abi files:

```
dxx -o apitest/apitest.wast apitest/apitest.cpp
dxx -g apitest/apitest.abi apitest/apitest.cpp
```

## 3. Deploy the contract

### 3.1 Open the wallet and connect to the nodes on the chain

```
cli_wallet -s ws://ip:port --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

Unlock the wallet
```
locked >>> unlock mylocalpassword
```

### 3.2 Import the private key of the wallet

```
unlocked >>> import_key nathan your_private_key
```

Deploy the contract helloworld

```
unlocked >>> deploy_contract apitest nathan 0 0 ./apitest DBX true
```
| Parameters | Interpretation |
| :--- | :--- |
| nathan | Account deploying the contract |
| 0 | Virtual machine type |
| 0 | Virtual machine version |
| ./apitest | path where wast/abi files are located |
| DBX | Commission asset type |
| true | Intiate broadcasting |
 
## 4. Call the contract

### Check the related api calling outcome 

```
unlocked >>> call_contract nathan apitest null show "{\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" DBX true

```
| Parameters | Interpretation |
| :--- | :--- |
| nathan | Account calling the contract |
| apitest | Which contract is called |
| null | Set up the commission for calling the contract |
| show | Which method in the contract is called |
| {\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" | Parameter of the method in the contract which is called |
| DBX | Commission asset type |
| true | Initiate broadcasting |

### Call the transferring interface

```
unlocked >>> call_contract nathan apitest null transfer "{\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" DBX true

```
| Parameters | Interpretation |
| :--- | :--- |
| nathan | Account calling the contract |
| apitest | Which contract is called |
| null | Set up the commission for calling the contract |
| transfer | Which method in the contract is called |
| {\"account_to\":\"alpha\", \"asset\":\"DBX\", \"amount\":\"50\"}" | Parameter of the method in the contract which is called |
| DBX | Commission asset type |
| true | Initiate broadcasting |

Check the related content of the transfer account
```
list_account_balances nathan
get_account_history nathan 100
```
It will show the log that nathan has transferred 50 DBX to alpha.
