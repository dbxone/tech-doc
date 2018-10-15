
### 设计原理
1. 合约代码： 暂时支持C++，后续会支持更多语言
2. 编译工具：llvm + binaryen， 将C++代码编译成wasm代码
3. 智能合约执行环境： WebAssembly作为底层执行VM，VM调用封装的API读取外部状态、读写外部存储。 wasm-jit 地址：https://github.com/WebAssembly/wasm-jit-prototype

### 合约编译工具(llvm + binaryen）
  1. clang编译
 ```
-emit-llvm选项告诉clang编译器生成LLVM中间代码
-emit-llvm -c选项告知编译器生成LLVM字节码二进制格式(a.bc)
-emit-llvm -S选项告知编译器生成LLVM字节码文本格式（a.ll）
```
  2. llvm-link链接，将多个LLVM二进制文件链接成一个LLVM二进制文件
  3. llc，可以把LLVM字节码的二进制格式文件（a.bc）转换为本地的汇编文件（a.s）
  4. binaryen + wasm jit  ==> wasm
  5. 合约部署时，wasm-jit将wast转换成wasm
  6. abi 生成工具（abi generator 可参考EOS实现)
  
wast生成方法：
````
1. clang -emit-llvm -O3 --std=c++14 --target=wasm32 .... 生成x.bc
2. llvm-link 将x.bc和contract lib链接成linked.bc
3. llc 生成汇编文件
4. binaryen 将汇编文件转成.wast
````


### 合约的创建和调用接口
#### 1. 部署(创建)合约 deploy_contract

```
{
  "ref_block_num": 14,
  "ref_block_prefix": 1713021572,
  "expiration": "2018-07-30T03:33:20",
  "operations": [[
      74,{
        "fee": { // 手续费
          "amount": 315234,
          "asset_id": "1.3.0"
        },
        "name": "abb", // 合约名
        "account": "1.2.17", // 发起部署合约的帐户id
        "vm_type": "0",  // vm type
        "vm_version": "0",   // vm version
        "code":   "0061736d01000000012d0960027f7e006000017f60027f7f017f60037f7f7f017f60017f0060017e0060000060037e7e7e0060017f017f02570503656e7610616374696f6e5f646174615f73697a65000103656e76066d656d637079000303656e76067072696e7473000403656e76077072696e747569000503656e7610726561645f616374696f6e5f646174610002030d0c020202070002080... ...
        1046a2802002202450d010240200241046a20004b0d00200220032802006a20004b0d030b2003410c6a22032001490d000b0b0f0b2000417c6a2203200328020041ffffffff07713602000b4901037f4100210502402002450d000240034020002d0000220320012d00002204470d01200141016a2101200041016a21002002417f6a22020d000c020b0b200320046b21050b20050b0300000b0b1b030041040b04006100000041100b0568692c20000041200b020a00",   // 合约的wasm代码
        "abi": {   // 合约ABI
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

手续费全局参数:
```
[
	74, {
		"fee": "10000", //标准手续费 
		"price_per_kbyte": 100000 // 根据消息体字节数大小(KB)，收取对应比例费用
	}
]
```
#### 2. 调用合约 call_contract
contract_call_operation
```
{
	"ref_block_num": 131,
	"ref_block_prefix": 3868272457,
	"expiration": "2018-07-19T08:38:10",
	"operations": [
		[75, {
			"fee": { // 手续费
				"amount": 1000,
				"asset_id": "1.3.0"
			},
			"account": "1.2.17", // 调用合约的帐户id
			"contract_id": "1.2.18", // 被调用的合约id
			"amount": { // 向合约发送的资产， 该amount字段为optional， 非必选
				"amount": 100000,
				"asset_id": "1.3.0"
			},
			"method_name": "deposit", // 合约方法名
			"data": "0d00000000000000", // 合约方法名需要的参数(根据合约abi进行序列化)
			"extensions": []
		}]
	],
	"extensions": [],
	"signatures": ["207d6e14beca57069470461f0ce3e25e679bd50714f5a2234d806fa8153d5f18505d6ad8939eb59d5071dfd2fbc4650cd8a330b3c780dfe23ba36fd4288ac087fc"]
}
```

手续费全局参数:
```
[
	75, {
		"basic_fee": "10000",
		"price_per_kbyte_ram": 100000, // 持久化存储使用量(单位为kb)
		"price_per_ms_cpu": 10 // CPU使用量（单位为ms）
	}
]
```
手续费：根据实际执行的CPU 、存储占用量，收取实际手续费。 若手续费不足，则交易失败，状态回滚。
合约执行失败，交易状态不会更新，同时节点不会继续广播该交易，交易不会打包进区块。

#### 3. 合约调用回执，写进区块
交易的operation_result中记录合约交易状态，成功或失败。
交易执行回执(打包进区块)：
```
"operation_results": [[
          3,{
            "billed_cpu_time_us": 787, // cpu time, 微秒
            "ram_usage_bs": 0, // 存储使用量, bytes
            "fee": {  // 手续费
              "amount": 1000,
              "asset_id": "1.3.0"
            }
          }
        ]
      ]

```

#### 4. 防ddos，收取交易手续费
  1. 根据cpu_usage使用量和存储使用量，计算实际手续费
  2. 每笔交易，设置max_transaction_cpu_usage 单个交易的CPU上限，全局参数（单个交易的cpu usage上限和单个区块的cpu usage上限）
  3. 限制合约执行deadline, 节点接收交易/打包区块时，验证deadline；验证区块/replay区块时，不验证deadline
  4. 创建合约手续费 = KB消息体大小 * 基准手续费
  5. 调用合约手续费 = CPU使用量 + 存储使用量 +   KB消息体大小 * 基准手续费



### 合约的充值提现
1. 向合约充值。 调用合约时，可以附带一定数量的资产，即消息体中的amount字段：

```
{
	"ref_block_num": 131,
	"ref_block_prefix": 3868272457,
	"expiration": "2018-07-19T08:38:10",
	"operations": [
		[75, {
			"fee": { // 手续费
				"amount": 1000,
				"asset_id": "1.3.0"
			},
			"account": "1.2.17", // 调用合约的帐户id
			"contract_id": "1.2.18", // 被调用的合约id
			"amount": { // 向合约发送的资产
				"amount": 100000,
				"asset_id": "1.3.0"
			},
			"method_name": "deposit", // 合约方法名，如果该deposit方法的payable属性为true，则可以接收充值； 否则合约调用失败
			"data": "0d00000000000000", // 合约方法名需要的参数(根据合约abi进行序列化)
			"extensions": []
		}]
	],
	"extensions": [],
	"signatures": ["207d6e14beca57069470461f0ce3e25e679bd50714f5a2234d806fa8153d5f18505d6ad8939eb59d5071dfd2fbc4650cd8a330b3c780dfe23ba36fd4288ac087fc"]
}
```
向合约充值的资产，累加到合约帐户的余额。合约代码对应的方法，实现为对应用户入帐的逻辑(由用户合约代码实现)，实现用户充值。

2. 合约内向外部帐户提现
为虚拟机封装的API提供了withdraw_asset方法，该方法只可以从合约帐户转出资产，转出资产数量不超过合约帐户余额。


3. 支持充值提现的transfer合约样例：
https://github.com/dbxone/dbxchain/tree/dev_master/contracts/examples/transfer



### 智能合约样例：

以helloworld合约为例，合约源代码：
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
////     /// @abi payable   此注释表示，hi文件可以接收充值。生成的abi中，对应的payable为true
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

合约abi:
```
{
  "____comment": "This file was generated by dbx-abigen. DO NOT EDIT - 2018-07-30T04:01:16",
  "version": "dbx::abi/1.0",
  "types": [],
  "structs": [{  // structs定义了合约的持久化存储表类型，和合约方法及参数类型
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
  "actions": [{ // 合约的方法
      "name": "hi",
      "type": "hi",
      "payable": false   // payable为false，该方法不接收资产
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
  "tables": [{ //合约的持久化表
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
