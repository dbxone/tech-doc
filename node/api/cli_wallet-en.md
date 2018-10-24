# cli_wallet Command list

| Command | Parameter | Explanation | Note |
| :--- | :--- | :--- | :--- |
| [set_password](cli_wallet/setpassword.md) | &lt;new_password&gt; | Set a new password to the wallet. You need to set a password when opening the wallet at the first time. |  |
| [unlock](cli_wallet/unlock.md) | &lt;my_password&gt; | Unlock the wallet |  |
| [import_key](cli_wallet/importkey.md) | &lt;account_name_or_id&gt;         &lt;true&gt; &lt;wif_private_key&gt; | Import the account private key to the wallet |  |
| [dump_private_keys](cli_wallet/dumpprivate-keys.md) |  | Print all the private key pairs owned by the wallet |  |
| [info](cli_wallet/getaccount.md) | &lt;account_name_or_id&gt; | Query the information of designated account, parameter can be the account name or id |  |
| [list_account_balances](cli_wallet/listaccount-balances.md) | &lt;account_name_or_id&gt; | Query account balance |  |
| [get_account_history](cli_wallet/getaccount-history.md) | &lt;account_name_or_id&gt;         &lt;limt_num&gt; | Query recent transaction record of the account |  |
| [get_relative_account_history](cli_wallet/getrelative-account-history.md) | &lt;account_name_or_id&gt;       &lt;start&gt; &lt;limit&gt; &lt;stop&gt; | Query recent transaction record of the account, support visiting next page |  |
| [get_account_history_by_operations](cli_wallet/getrelative-account-history_by_operations.md) | &lt;account_name_or_id&gt; &lt;\[\]&gt;  &lt;start&gt; &lt;limit_num&gt; | Query recent transaction record of the account according to oeration_type, and return the txID corresponding to operation |  |
| [transfer](cli_wallet/transfer.md) | &lt;from_account&gt;                   &lt;to_account&gt; &lt;amount&gt;     &lt;DBX&gt; &lt;memo&gt; &lt;true&gt; | Transfer |  |
| [transfer2](cli_wallet/transfer2.md) | &lt;from_account&gt;                   &lt;to_account&gt; &lt;amount&gt;     &lt;DBX&gt; &lt;memo&gt; &lt;true&gt; | Transfer, parameter similar to transfer, the return including the currenct transaction id |  |
| [get_block](cli_wallet/getblock.md) | &lt;block_num&gt; | Acquire the information of designated block |  |
| [info](cli_wallet/info.md) |  | Acquire the blockchian information, able to find the newest block height by this command |  |
| [help](cli_wallet/help.md) |  | Help command, which will return all the interfaces supported by the wallet |  |
| [gethelp](cli_wallet/gethelp.md) | &lt;command&gt; | Help command,Find the calling method of the designated wallet command |  |

## Calling case

Command line wallet cli_wallet connects to witness_node:
```
cli_wallet -w wallet.json -s ws://127.0.0.1:38090 -r 127.0.0.1:38091 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```
First you need to set a password fot your wallet (This is a local password which is used to unlock the wallet)：

```
new >>> set_password my_password
```

It will show as follows when it executes susccessfully:
```
locked >>>
```

Unlock the wallet:
```
locked >>> unlock my_password
```

It will show as follows when it is unlocked successfully：
```
unlocked >>>
```

You can find the synchronous status of the current block using info command
```
unlocked >>> info
info
{
  "head_block_num": 13845,
  "head_block_id": "000036155a3877d925a485a53c389337b526f6c5",
  "head_block_age": "0 second old",
  "next_maintenance_time": "6 minutes in the future",
  "chain_id": "6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d",
  "participation": "100.00000000000000000",
  "active_witnesses": [
    "1.6.1",
    "1.6.2",
    "1.6.3",
    "1.6.4",
    "1.6.5",
    "1.6.6",
    "1.6.7",
    "1.6.8",
    "1.6.9",
    "1.6.10",
    "1.6.11"
  ],
  "active_committee_members": [
    "1.5.0",
    "1.5.1",
    "1.5.2",
    "1.5.3",
    "1.5.4",
    "1.5.5",
    "1.5.6",
    "1.5.7",
    "1.5.8",
    "1.5.9",
    "1.5.10"
  ]
}
```


## jsonrpc calling case

Enter command line（cmd），calling by curl

```
curl --data '{"jsonrpc": "2.0", "method": "info", "params": [], "id": 1}' http://127.0.0.1:38091
```

It will show the return

### POST request case

Request URL as follows

```
http://127.0.0.1:38091
```

Requesting subjective

```
{"jsonrpc": "2.0", "method": "info", "params": [], "id": 1}
```

Note：The format of params is`[API type，API instruction，parameter]`


Return

```
{
    "id":1,
    "jsonrpc":"2.0",
    "result":{
        "head_block_num":13862,
        "head_block_id":"0000362698890c172bf31b055908a102c3b7df45",
        "head_block_age":"3 seconds old",
        "next_maintenance_time":"5 minutes in the future",
        "chain_id":"6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d",
        "participation":"100.00000000000000000",
        "active_witnesses":[
            "1.6.1",
            "1.6.2",
            "1.6.3",
            "1.6.4",
            "1.6.5",
            "1.6.6",
            "1.6.7",
            "1.6.8",
            "1.6.9",
            "1.6.10",
            "1.6.11"
        ],
        "active_committee_members":[
            "1.5.0",
            "1.5.1",
            "1.5.2",
            "1.5.3",
            "1.5.4",
            "1.5.5",
            "1.5.6",
            "1.5.7",
            "1.5.8",
            "1.5.9",
            "1.5.10"
        ]
    }
}
```
