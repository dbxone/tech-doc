# The first smart contract program helloworld

## 1. [Source code](https://github.com/dbxone/dbxchain/blob/contract/contracts/examples/helloworld/helloworld.cpp)

The source code of helloworld can also be generated utilizing the dxx mode:

```
dxx -n helloworld
```

The code is as follows:
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

## 2. Complie the contract, generate wast and abi

Complie the contract, generate wast and abi files:

```
dxx -o helloworld/helloworld.wast helloworld/helloworld.cpp
dxx -g helloworld/helloworld.abi helloworld/helloworld.cpp
```

## 3. Deploy the contract

### 3.1 Open the wallet, connect to the nodes on the chain.

```
cli_wallet -s ws://ip:port --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

Unlock the wallet
```
locked >>> unlock mylocalpassword
```

### 3.2 Import the private key of the wallet

```
unlocked >>> import_key your_account_name your_private_key
```

Deploy the contract helloworld

```
unlocked >>> deploy_contract helloworld your_account_name 0 0 ./helloworld DBX true
```
| Parameters | Interpretation |
| :--- | :--- |
| your_account_name | Account deploying the contract |
| 0 | Virtual machine type |
| 0 | Virtual machine version |
| ./helloworld | Path where wast/abi files are located |
| DBX | Commission asset type |
| true | Initiate broadcasting |
 
## 4. Call the contract

```
unlocked >>> call_contract your_account_name helloworld null hi "{\"user\":\"abcdefg\"}" DBX true

```
| Parameters | Interpretation |
| :--- | :--- |
| your_account_name | Account calling the contract |
| helloworld | which contract is called |
| null | Set up commission needed for calling the contract |
| hi | Which method in the contract is called |
| "{\"user\":\"abcdefg\"} | Parameter of the method in the contract which is called |
| DBX | Commission asset type |
| true | Initiate broadcasting |


## 5. Outcome

Run the log at the witness_node to check the running information as follows:

```
[(20,hi)->20] CONSOLE OUTPUT BEGIN =====================
hi, abcdefg

[(20,hi)->20] CONSOLE OUTPUT END =====================
```

Here, the smart contract id of helloworld is 20.
