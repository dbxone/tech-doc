# Compilation, deployment and running of the smart contracts

## 1. Compile the contract

Create a helloworld contract utilizing the dxx mode:

```
dxx -n helloworld
```

## 2. Compile the contract, generate wast and abi

Compile the contract, generate wast and abi files:

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
| your_accoutn_name | Account deploying the contract |
| 0 | Virtual machine type |
| 0 | Virtual machine version |
| ./helloworld | Path where wast/abi files are located |
| DBX | Commission asset type |
| true | Initiate broadcasting |
 
## 4. Call the contract

```
unlocked >>> call_contract your_accoutn_name helloworld null hi "{\"user\":\"abcdefg\"}" DBX true

```
| Parameters | Interpretation |
| :--- | :--- |
| your_accoutn_name | Account calling the contract |
| helloworld | Which contract is called |
| null | Set up commission needed for calling the contract |
| hi | Which method in the contract is called |
| "{\"user\":\"abcdefg\"} | Parameter of the method in the contract which is called |
| DBX | Commission asset type |
| true | Initiate broadcasting |
