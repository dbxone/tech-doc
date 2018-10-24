## Smart contract introduction

DBXChain smart contract 2.0，WebAssembly virtual machine as the basement technology and currently supporting the smart contract compiling in C++ language.
Developers compile smart contracts in C++ language, convert the code to WebAssembly (WASM) by llvm then deploy it on the blockchain, finally realizes interaction through smart contract ABI (Application Binary Interface).

# Contract account design
  1. There are two types of accounts：Common account and contract account
  2. Contract account, established by common account through deploying contracts, does not have private key so that the asset access is controlled by the contract code
  3. Contract account objective, code field stores contract code, abi stores contract code and abi
  4. COntract code does not support any update

# Sustainable storage of the contract
  1. Define the data storage format of the contract; define the linear storing space, every element is one struct type
  2. The sustainable storage mechanism of the contract is put into RAM when the witness_node is running; it is written into the disk when the program is quitted; RAM optimization could be considered in later period (disk+cache).
  3. Envelope the API which support sustainable reading and writting storage, providing the interface of reading, writing, searching method to be called
  4. The contract can only write its own storing space and read other contracts' storing 合约只能写自己的存储空间，可以读其它合约的存储空间，但不可直接写；  同一合约内不同帐户的存储空间，由用户合约代码控制权限
  5. 合约内可以根据区块号获取区块，读取外部状态

# 智能合约公共库，供智能合约在虚拟机内部调用
 1. 提供API，获取head block num,  获取head block id
 2. get_balance 获取外部帐户余额
 3. 加解密API、验签API
 4. 持久化存储API

# 销毁合约(暂不支持)
合约内可以提供销毁方法，如：
selfdestruct(string account) 将资产转至recipient帐户，然后销毁合约
回收的存储空间，按全局手续费参数计算，奖励给合约创建者(从系统资金池中获取,  最多返还存储价格的20%)。

# 合约调用合约(暂不支持)
目前只能由普通帐户和合约帐户交互，不支持合约间交互。

# 技术实现
1. 合约代码： 暂时支持C++，后续会支持更多语言
2. 编译工具：llvm + binaryen， 将C++代码编译成wasm代码
3. 智能合约执行环境： WebAssembly作为底层执行VM，VM调用封装的API读取外部状态、读写外部存储。 wasm-jit 地址：https://github.com/WebAssembly/wasm-jit-prototype
