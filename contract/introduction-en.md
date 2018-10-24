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
  4. The contract can only write its own storing space and read other contracts' storing space but cannot directly write other contracts' storing space; The access to the storing space of different accounts in one contract is controlled by the contract code
  5. In the contract, you can acquire blocks and read external status according to their block number

# Public library of smart contracts, used for calling smart contracts in the virtual machine
 1. Offer API，acquire head block num, acquire head block id
 2. get_balance Acquire balance of the external account
 3. encipher and decipher API, verify and sign API
 4. Store API sustainably

# Destruct contract (Not supported yet)
Contracts could provide destructing methods internally, for example：
selfdestruct(string account) Transfer asset to the recipient account then destruct the contract
Recycling storing space, computed based on the global commission parameter and the contract creater get rewarded (The reward is from system bonus pool and can return 20% of the storing price at most).

# Contract calls contract (Not supported yet)
Only the interaction between common accounts and contract accounts is supported but not the interaction between contracts currently.

# Technical realization
1. Contract code： Only support C++ temporarily, will add more languages in the following steps
2. Compiling tool：llvm + binaryen， convert C++ code to wasm code
3. Smart contract executing environment： WebAssembly as the basement executing VM, VM calls the enveloped API to read external status, read and write external storage. wasm-jit address：https://github.com/WebAssembly/wasm-jit-prototype
