# This contract is used to call the hi method of helloworld

## 1. [Source code](https://github.com/dbxone/dbxchain/blob/contract/contracts/examples/call-helloworld/call-helloworld.cpp)

The code is as follows:
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

## 2. Compile the contract, generate wast and abi

Compile the contract, generate wast and abi files:

```
dxx -o call-helloworld/call-helloworld.wast call-helloworld/call-helloworld.cpp
dxx -g call-helloworld/call-helloworld.abi call-helloworld/call-helloworld.cpp
```

## 3. Deploy the contract

### 3.1 Open the wallet, connect to nodes on the chain.

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

Deploy the contract

```
unlocked >>> deploy_contract call-helloworld nathan 0 0 ./call-helloworld DBX true
```
| Parameters | Interpretation |
| :--- | :--- |
| nathan | Account deploying the contract |
| 0 | Virtual machine type |
| 0 | Virtual machine version |
| ./call-helloworld | Path wherer wast/abi files are located |
| DBX | Commission asset type |
| true | Initiate broadcasting |
 
## 4. Call the contract

```
unlocked >>> call_contract nathan call-helloworld null call_hi "{\"act_id\":20}" DBX true

```
| Parameters | Interpretation |
| :--- | :--- |
| nathan | Account calling the contract |
| call-helloworld | Which contract is called |
| null | Set up commission needed for calling the contract |
| call_hi | Which method in the contract is called |
| "{\"act_id\":20}" | Parameter of the method in the contract which is called |
| DBX | Commission asset type |
| true | Initiate broadcasting |


## 5. Outcome

Run the log at witness_node to check the running information as follows:

```
[(21,call_hi)->21] CONSOLE OUTPUT BEGIN =====================
hi contract:20

[(21,call_hi)->21] CONSOLE OUTPUT END =====================

... ...

[(20,hi)->20] CONSOLE OUTPUT BEGIN =====================
hi

[(20,hi)->20] CONSOLE OUTPUT END =====================
```

It will show the hi method of helloworld is called.
