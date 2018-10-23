### Design principles
1. Contract code： Only support C++ temporarily，will add more languages in the following
2. Compiling tool：llvm + binaryen， Compile the C++ code to the wasm code
3. Smart contract executing evironment： WebAssembly serves as the basement executing VM，VM calls the enveloped API to read the external status as well as read and write the external storage. wasm-jit address：https://github.com/WebAssembly/wasm-jit-prototype

### Contract compiling tool (llvm + binaryen）
  1. clang Compilation
 ```
-emit-llvm option tells the clang compiler to generate the LLVM intermediary code
-emit-llvm -c option tells the compiler to generate the LLVM byte code in the binary format (a.bc)
-emit-llvm -S option tells the compiler to generate the LLVM byte code in the text format（a.ll）
```
  2. llvm-link link，connect multiple LLVM binary files to one LLVM binary file
  3. llc，able to convert the LLVM byte code file in binary format （a.bc）to the local compling file（a.s）
  4. binaryen + wasm jit  ==> wasm
  5. When deploying the contract, wasm-jit converts wast to wasm
  6. abi generator（abi generator could be realized referring to EOS)
  
wast generating method：
````
1. clang -emit-llvm -O3 --std=c++14 --target=wasm32 .... generates x.bc
2. llvm-link connects x.bc and contract lib to become linked.bc
3. llc generates the compiling file
4. binaryen converts the compiling file to .wast
````


### Create the contract and call the interface
#### 1. Deploy(Create) contract deploy_contract

```
{
  "ref_block_num": 14,
  "ref_block_prefix": 1713021572,
  "expiration": "2018-07-30T03:33:20",
  "operations": [[
      74,{
        "fee": { // Commission
          "amount": 315234,
          "asset_id": "1.3.0"
        },
        "name": "abb", // Contract name
        "account": "1.2.17", // Account id initiating the contract deployment
        "vm_type": "0",  // vm type
        "vm_version": "0",   // vm version
        "code":   "0061736d01000000012d0960027f7e006000017f60027f7f017f60037f7f7f017f60017f0060017e0060000060037e7e7e0060017f017f02570503656e7610616374696f6e5f646174615f73697a65000103656e76066d656d637079000303656e76067072696e7473000403656e76077072696e747569000503656e7610726561645f616374696f6e5f646174610002030d0c020202070002080... ...
        1046a2802002202450d010240200241046a20004b0d00200220032802006a20004b0d030b2003410c6a22032001490d000b0b0f0b2000417c6a2203200328020041ffffffff07713602000b4901037f4100210502402002450d000240034020002d0000220320012d00002204470d01200141016a2101200041016a21002002417f6a22020d000c020b0b200320046b21050b20050b0300000b0b1b030041040b04006100000041100b0568692c20000041200b020a00",   // wasm code of the contract
        "abi": {   // Contract ABI
          "version": "dbx::abi/1.0",
          "types": [],
          "structs": [{
              "name": "hi",
              "base": "",
              "fields": [{
                  "name": "user",
                  "type": "uint64"
                }
              ]
            }
          ],
          "actions": [{
              "name": "hi",
              "type": "hi",
              "payable": false
            }
          ],
          "tables": [],
          "error_messages": [],
          "abi_extensions": []
        },
        "extensions": []
      }
    ]
  ],
  "extensions": [],
  "signatures": [
    "201ac9a0c1fc8142e0a9e288b7ec692a4f8b367893fd97608e60e28f073d74a5842c2dca4810d839742c0639074dd288e21d60558637df4c30e823379d0e010c3a"
  ]
}
```

Commission global parameter:
```
[
	74, {
		"fee": "10000", //Standard commission 
		"price_per_kbyte": 100000 // Charge the corresponding commission according to the byte size of the message (KB)
	}
]
```
#### 2. Call the contract call_contract
contract_call_operation
```
{
	"ref_block_num": 131,
	"ref_block_prefix": 3868272457,
	"expiration": "2018-07-19T08:38:10",
	"operations": [
		[75, {
			"fee": { // Commission
				"amount": 1000,
				"asset_id": "1.3.0"
			},
			"account": "1.2.17", // Account id calling the contract
			"contract_id": "1.2.18", // Contract id which is called
			"amount": { // Asset sent to the contract, the amount field is optional
				"amount": 100000,
				"asset_id": "1.3.0"
			},
			"method_name": "deposit", // Contract method name
			"data": "0d00000000000000", // parameters needed by the contract method name ( Serializing based on contract abi)
			"extensions": []
		}]
	],
	"extensions": [],
	"signatures": ["207d6e14beca57069470461f0ce3e25e679bd50714f5a2234d806fa8153d5f18505d6ad8939eb59d5071dfd2fbc4650cd8a330b3c780dfe23ba36fd4288ac087fc"]
}
```

Commission global parameter:
```
[
	75, {
		"basic_fee": "10000",
		"price_per_kbyte_ram": 100000, // Store the using amount sustainably (in kb unit)
		"price_per_ms_cpu": 10 // CPU using amount（in ms unit）
	}
]
```
Commission：Commission is charged according to the practically executed CPU and RAM occupation. If the commission is insufficient, the transaction fails and the status is rolled back.
If the contract fails to execute, the transaction status will not be updated and nodes will not continue to broadcast the failed transaction, neither will the transaction be packed into the block.

#### 3. Contract calling receipt, written into the block
Operation_result of the transaction records the contract transaction status, successful or failed.
Transaction execution receipt (packed into the block)：
```
"operation_results": [[
          3,{
            "billed_cpu_time_us": 787, // cpu time, microsecond
            "ram_usage_bs": 0, // RAM occupation, bytes
            "fee": {  // Commission
              "amount": 1000,
              "asset_id": "1.3.0"
            }
          }
        ]
      ]

```

#### 4. DDPoS，charging the transaction commission
  1. Compute the real commission according to cpu_usage and RAM occupation
  2. For each transaction, set up max_transaction_cpu_usage as the CPU upper limit for single transaction, global parameter（cpu usage upper limit of single transaction and cpu usage upper limit of single block）
  3. Restrict the contract execution deadline, verify the deadline when the node accepts transaction/packs blocks；do not verify the deadline when verifying blocks/ replaying blocks
  4. Commission needed for creating a contract= KB size of the message * standard commission
  5. Commission needed for calling a contract= CPU occupation + RAM occupation +   KB message size * standard commission



### Charge and withdrawal of the contract
1. Charge the contract. When calling a contract, you can attach certain amount of asset, namely the amount field in the message：

```
{
	"ref_block_num": 131,
	"ref_block_prefix": 3868272457,
	"expiration": "2018-07-19T08:38:10",
	"operations": [
		[75, {
			"fee": { // Commission
				"amount": 1000,
				"asset_id": "1.3.0"
			},
			"account": "1.2.17", // Account id calling the contract
			"contract_id": "1.2.18", // Contract id which is called
			"amount": { // Asset sent to the contract
				"amount": 100000,
				"asset_id": "1.3.0"
			},
			"method_name": "deposit", // Contract method name, if the payable attribution of the deposit method is true, the charge is acceptable; otherwise the contract call fails.
			"data": "0d00000000000000", // Parameters needed by the contract method(Serializing based on contract abi)
			"extensions": []
		}]
	],
	"extensions": [],
	"signatures": ["207d6e14beca57069470461f0ce3e25e679bd50714f5a2234d806fa8153d5f18505d6ad8939eb59d5071dfd2fbc4650cd8a330b3c780dfe23ba36fd4288ac087fc"]
}
```
Asset charged to the contract will accumulates to the balance of the contract account. The method corresponding to the contract code will realize the logic to transfer asset to the corresponding user (it is realized by the user's contract code), and realize charging by the user.

2. External withdrawal from the contract
Offer withdraw_asset method to the API enveloped by the virtual machine，which can only transfer asset out of the contract account and the transferring amount cannot exceed account balance.


3. Transferring contract sample supporting charing and withdrawing：
https://github.com/dbxone/dbxchain/tree/dev_master/contracts/examples/transfer



### Smart contract sample：

Regard helloworld contract as an example, the source code of the contract is：
```
#include <dbxlib/contract.hpp>
#include <dbxlib/dispatcher.hpp>
#include <dbxlib/print.hpp>
#include <dbxlib/types.h>

using namespace graphene;

class hello : public contract
{
  public:
    hello(account_name n)
        : contract(n)
    {
    }

    /// @abi action
////     /// @abi payable   The annotation means hi file could accept charging. The corresponding payable is true in the generated abi
    void hi(uint64_t user)
    {
        for (int i = 0; i < 2; ++i) {
            print("hi, ", user, "\n");
        }
    }
       /// @abi action
    void bye(uint64_t user)
    {
        for (int i = 0; i < 2; ++i) {
            print("bye, ", user, "\n");
        }
    }

};

DBX_ABI(hello, (hi)(bye))
```

Contract abi:
```
{
  "____comment": "This file was generated by dbx-abigen. DO NOT EDIT - 2018-07-30T04:01:16",
  "version": "dbx::abi/1.0",
  "types": [],
  "structs": [{  // structs defines the type of sustainable contract storage, contract method and parameter type
      "name": "account",
      "base": "",
      "fields": [{
          "name": "owner",
          "type": "uint64"
        },{
          "name": "balances",
          "type": "contract_asset[]"
        }
      ]
    },{
      "name": "hi",
      "base": "",
      "fields": [{
          "name": "user",
          "type": "uint64"
        }
      ]
    },{
      "name": "deposit",
      "base": "",
      "fields": []
    },{
      "name": "withdraw",
      "base": "",
      "fields": [{
          "name": "to_account",
          "type": "uint64"
        },{
          "name": "contract_asset_id",
          "type": "uint64"
        },{
          "name": "amount",
          "type": "int64"
        }
      ]
    }
  ],
  "actions": [{ // Contract method
      "name": "hi",
      "type": "hi",
      "payable": false   // payable为false，this method does not accept asset
    },{
      "name": "deposit",
      "type": "deposit",
      "payable": true
    },{
      "name": "withdraw",
      "type": "withdraw",
      "payable": false
    }
  ],
  "tables": [{ //the sustainable table of the contract
      "name": "account",
      "index_type": "i64",
      "key_names": [
        "owner"
      ],
      "key_types": [
        "uint64"
      ],
      "type": "account"
    }
  ],
  "error_messages": [],
  "abi_extensions": []
}
```
