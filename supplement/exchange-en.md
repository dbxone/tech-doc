### 3. Starting witness_node, synchronze data

Enter dbx directory, start DBXChain witness_node

```
# 2 parameters could be used to save RAM occupation： --track-account and --partial-operations=true
nohup ./programs/witness_node/witness_node --data-dir=trusted_node --rpc-endpoint=127.0.0.1:38090 \
--p2p-endpoint=0.0.0.0:38091 --log-file --track-account "\"1.2.2999\""  --track-account "\"1.2.3000\"" \
--partial-operations=true >>witness.out 2>&1 &

# Export the log file, if it does not exist, the log will be exported to the console
--log-file 

```

Right now all-node program occupies 12GB+ RAM, using two parameters --track-account account_id\(here is the account id in 1.2.x format\) and --partial-operations=true to run the program, only transaction history of the exchange account will be saved in RAM so that the RAM occupation can be less than 4GB.

```



### 4. Run the command line wallet cli_wallet

Command line wallet cli_wallet connects to witness_node:

```
./programs/cli_wallet/cli_wallet -s ws://127.0.0.1:38090 \
--enable-rpc-log -r 127.0.0.1:38091 --data-dir=trusted_node
```

cli_wallet initiating parameter：

```
# websocket rpc address connected to the witness node
-s

# Export rpc log file
--enable-rpc-log

# websocket rpc address provided by cli_wallet, start API service of cli_wallet
# Note：Do not set 0.0.0.0, because all hosts can access your wallet.
-r 127.0.0.1:38091

# Running in the progress awaiting mode
-d 

& Meaning the program is running at the back desk
```

First you need to set a password for your wallet\(This is a local password which is used to unlock the wallet\)：

```
new >>> set_password my_password
# Once the execution is successful, it will show:
locked >>>
# The unlock the wallet:
locked >>> unlock my_password
# Once unlocking successfully, it will show：
unlocked >>>
```

Use info command to find the synchronizing status of the current block

```
unlocked >>> info
info
{
  "head_block_num": 3913758,
  "head_block_id": "003bb81eec2abfdb2cf58ffdf4dd547ea190530e",
  "head_block_age": "3 seconds old",
  "next_maintenance_time": "0 second ago",
  "chain_id": "4f7d07969c446f8342033acb3ab2ae5044cbe0fde93db02de75bd17fa8fd84b8",
  "participation": "100.00000000000000000",
  ...
 }
 # head_block_age represents the newest block time, the system generates a new block every three seconds
 # participation means the participating rate of the witness, which should be greater than 70 to ensure the network is healthy
```


### 5. Use command line wallet cli_wallet, import the private key of the account

If you don't have any account, downlod DBXChain light weighted wallet first or access online wallet to register an account\(Remember to back it up，save your private key properly\).



### 6. Run cli_wallet at back desk

After importing the private key of the wallet, ctrl + c to exit, it will create the local wallet file at this moment. Restart with parameter -d &, shown as follows：

```
nohup ./programs/cli_wallet/cli_wallet -s ws://127.0.0.1:38090 \
--enable-rpc-log -r 127.0.0.1:38091 -d >>wallet.out 2>1 &
```

After the above commands, press "Enter" again, then enter "exit" in shell to exit the endpoint. Related console output is redirected to wallet.out file.

## Four. Query transaction history of the account, monitor user's charge

#### Query the transaction history and acquire the txID of the transaction by the account 

cli_wallet provides not only command line interface, but also json rpc interface. When the wallet opens API service in http rpc mode, it is same as entering commands in the wallet. It could be called through wscat or using http client\(such as curl\).

Hereby, method imports the command name, params array imports the parameter list\(params imports void array if no parameter\), id is the request mark, and the result id should be consistent with the request id. If the execution is successful, there will be result, otherwise error happens

cli_wallet provides 3 interfaces to query transaction history：get_account_history, get_relative_account_history and get_account_history_by_operations. Thereinto, get_account_history_by_operations can return transaction id\(txID\). The three interfaces have detailed explanation in [wallet api introduction document](https://doc.dbx.io/core/ming-ling-xing-qian-bao-cli-wallet-api-shuo-ming.html). Regard get_account_history_by_operations as an example, the steps are shown as follows：

1. Unlock the wallet.
2. Find the account id by its name.
3. Query the transaction history according to the account id.

**Detailed process is shown as follows, regrad account dbx-light as an example**：

#### 1. Unlock the wallet:

###### request：

```
// unlock unlock the wallet，my_password is the unlocking password
curl --data '{"jsonrpc": "2.0", "method": "unlock", "params": ["my_password"], "id": 1}' http://127.0.0.1:38091/rpc
```

Unlock susccessfully, return：

```
{"id":1,"jsonrpc":"2.0","result":null}
```

#### 2. Acquire the account id of dbx-light:

If the account id is known, skip this step.

###### request：

```
// get_account_id，the imported parameter is the account name or id
curl --data '{"jsonrpc": "2.0", "method": "get_account_id", "params": ["dbx-light"], "id": 1}' http://127.0.0.1:38091/rpc
```

The returning result is as follow, among which the account id is 1.2.3054, "1.2." means the type is account：

```
{"id":1,"result":"1.2.3054"}
```

#### 3. Call the get_account_history_by_operations interface of the wallet, query transaction history of the account, the returning information contains txID: 

If unlock is not called, the resulting transfer transaction memo can not be deciphered. Hereby, only both transaction parites can decipher the memo.

###### request：

```
// get_account_history_by_operations The first parameter is the account id，the second one is operation array，which could be [], the third one is the beginning serial number, the fourth one is limit，which means recent "limit" transaction history
curl --data '{"jsonrpc": "2.0", "method": "get_account_history_by_operations", "params": ["1.2.3054",[], 1, 10], "id": 1}' http://127.0.0.1:38091/rpc
```

###### response：

```
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": {
    "total_without_operations": 3, // This number usually does not equal to the imported limit, meaning how many transactions are actually found before filtered by operation array; If the number is less than limit，it means the newest transaction is found
    "details": [{ //  Returned details is an array, each item is one transaction
      "memo": "196702323",  // This is deciphered memo, only both transaction parties can decipher the memo
      "description": "Transfer 3099 DBX from dbx-light to yunbi-dbx -- Memo: 196702323   (Fee: 0.09493 DBX)", //Transaction description
      "op": {  // Operation contained in the transaction
        "id": "1.11.3436",
        "op": [0, {// 0 means transfer
          "fee": {
            "amount": 9493,// Operation payment fee is (9493/100000) DBX, the number must be divided by 100000
            "asset_id": "1.3.1" //  Asset 1.3.1 is DBX
          },
          "from": "1.2.3054",// Transferring account
          "to": "1.2.2999",// Receiving account
          "amount": {
            "amount": 300000,  // Transfer amount (300000/100000) namely 3 DBX ，the number must be divided by 100000
            "asset_id": "1.3.1"
          },
          "memo": {
            "from": "DBX68o9LkFKv5ihSt6z9oTmc7wVALUmT5Kd75BTy9rMp38wSuWU5N",
            "to": "DBX5yRwAseZhPBorMmxXhQvmvsDzoJJbQnau5fFboGr5V2zGZPWsk",
            "nonce": "384187316390066",
            "message": "1c05a47a362361c0cf2dba52d08f3517"  // This is encrypted memo
          },
          "extensions": []
        }],
        "result": [0, {}],
        "block_num": 1115034, // Which block the transaction is packed into, the block number (block height)
        "trx_in_block": 0,// Transaction location in the block index
        "op_in_trx": 0,
        "virtual_op": 3482
      },
      "transaction_id": "f9f8f8359c59ac1341516facdf30c98fd5d57b5b"
    }, {
      "memo": "",
      "description": "Transfer 7100 DBX from yunbi-dbx to dbx-light   (Fee: 1 DBX)",
      "op": {
        "id": "1.11.3331",
        "op": [0, {
          "fee": {
            "amount": 100000,
            "asset_id": "1.3.0"
          },
          "from": "1.2.2999",
          "to": "1.2.3054",
          "amount": {
            "amount": 710000000,
            "asset_id": "1.3.1"
          },
          "extensions": []
        }],
        "result": [0, {}],
        "block_num": 1000766,
        "trx_in_block": 0,
        "op_in_trx": 0,
        "virtual_op": 3377
      },
      "transaction_id": "7c64c51ee931043ca1bc6791efc942e94b8236af"
    }]
  }
}
```

**Note：As to the exchange, the asset id of the transfer operation must be 1.3.1\(DBX\).**

#### Irrevocable block

Call get_dynamic_global_properties interface of cli_wallet, find the current biggest irrevocable block number\(Namely the biggest irrevocable block height\). Transactions packed into blocks less than such height are all confirmed and irrevocable. It can be used as reference when users want to withdraw, process the withdrawal only if the block is irrevocable.

```
curl --data '{"jsonrpc": "2.0", "method": "get_dynamic_global_properties", "params": [], "id": 1}' http://127.0.0.1:38091/rpc
```

Return：

```
{
  "id": 1,
  "result": {
    "id": "2.1.0",
    "head_block_number": 1724515, // Current biggest block number (block height)
    "head_block_id": "001a506300f6717c3e99b6d8d89b264d94f1793c",
    "time": "2017-08-16T14:51:53",
    "current_witness": "1.6.2",
    "next_maintenance_time": "2017-08-16T15:00:00",
    "last_budget_time": "2017-08-16T14:50:00",
    "witness_budget": 0,
    "accounts_registered_this_interval": 0,
    "recently_missed_count": 1,
    "current_aslot": 2426557,
    "recent_slots_filled": "326968992855967788277935148493325729655",
    "dynamic_flags": 0,
    "last_irreversible_block_num": 1724507   // The biggest irrevocable block number (block height) is 1724507
  }
}
```

## Six. Reminder

1. User charge. Every transfer could have one memo, which is used to identify which user charge it is by the exchange. Detailed memo relates to the exchange user, depending on the exchange freely. The memo is encrypted, only both transferring parties could decipher it.
2. Transfer commission. It is composed of two parts：basic commission + memo cost, among which basci commission is 0.05DBX, memo cost is determined by total byte length, 0.5DBX/`KB`. Compute the commission for one transaction as：`0.05 + 0.5*(KBs of memo) DBX, only reserve the integar KB`. Commission of the transfer with memo usually rang between\[0.05, 0.15\] DBX\(Suppose the memo length is no more than 100 bytes\).
3. When the exchange queries transaction history and processes user charge, it needs to deal with the special cases which is filled in the memo by the user. For exmaple, the memo provided by the exchange to the user is 1234567, while the memo filled by the user is "My memo is 1234567!", such cases needs to be considered.
4. It's not recommended for the exchange to provide memo similar to DBX123456, taking memo as the account to charge.
   **There is no restriction against the length and content of the memo, it is recommended the length is more than 10 characters with number initial**.
5. json rpc interface of the wallet, the account name should be in lowercase letters without any capitals. When the user withdraws to DBX, it needs to convert the binded account name to lowercase letters.
6. **Artificially process problems of user charging**：Users need to provide txID\(users can check the current transfer information by their wallets to get it\)，txID can ensure the uniqueness of transfer charging by users. Please note：**The platform stores artificially processed txID, one txID can only process ** once. It will be regarded as fraud if different registered users submit orders using the same txID!
7. There are multiple assets in the system, among which asset id（asset_id）1.3.1 is DBX. Monitoring the charge by the user, please check the asset_id field in the transfer transaction is 1.3.1.
8. User withdrawal. When calling transfer/transfer2 to process user withdrawing, please import a series of fields representing the transfer amount with double quotation marks. It is shown as follows：
9. ```
   curl --data '{"jsonrpc": "2.0", "method": "transfer2", "params": ["from_account", "to_account", "100.01", "DBX", "",  true], "id": 1}' http://127.0.0.1:38091/rpc
   ```
10. DBX accuracy, rounded to the 5 decimals, namely the smallest unit is 0.00001 DBX. There is no decimal on DBXChain, all numbers are multiplied with 100,000, so the number returned from get_account_history / get_account_history_by_operations interfaces, such as the transfer amount should be divided by 100,000 to get the real number.
11. Only query functionality is available when the wallet status is locked while the transfer and transfer memo deciphering is not available. You need to unlock the wallet before transferring or querying the transaction history.
12. **When transfer/transfer2 is processing the transfer, if the third parameter, namely the transfer amount, contains decimals, double quotation marks should be added, otherwise the transfer would fail. It is recommended that all transfer amounts added with double quotation marks.**

##### Related document：

1. [witness_node initiating script(http://dbx-package.oss-cn-hangzhou.aliyuncs.com/dbxchain/script/witness_start.sh)
2. [cli_wallet initiating script](http://dbx-package.oss-cn-hangzhou.aliyuncs.com/dbxchain/script/wallet_start.sh)
3. [back-up cli_wallet initiating script](http://dbx-package.oss-cn-hangzhou.aliyuncs.com/dbxchain/script/start_backup_wallet.exp)，the script provides 3 connecting point to the main net, if local witness_node is not available temporarily, this script could be run to connect to the main net.
4. [DBXChain cold wallet offline signature workshop](https://doc.dbx.io/core/dbxleng-qian-bao-li-xian-qian-ming.html)
5. [wallet api introduction document](https://doc.dbx.io/core/ming-ling-xing-qian-bao-cli-wallet-api-shuo-ming.html)
