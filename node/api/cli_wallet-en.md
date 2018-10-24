# cli_wallet Command list

| 命令 | 参数 | 说明 | 备注 |
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
| [get_block](cli_wallet/getblock.md) | &lt;block_num&gt; | 获取指定区块信息 |  |
| [info](cli_wallet/info.md) |  | 获取区块链信息，可以用此命令查询最新区块高度 |  |
| [help](cli_wallet/help.md) |  | 帮助命令，此命令会返回钱包支持的所有接口 |  |
| [gethelp](cli_wallet/gethelp.md) | &lt;command&gt; | 帮助命令，查看指定钱包命令的调用方法 |  |

## 调用示例

命令行钱包cli_wallet连接witness_node:
```
cli_wallet -w wallet.json -s ws://127.0.0.1:38090 -r 127.0.0.1:38091 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```
首先需要为钱包设置一个钱包密码(这个密码是本地的，用来解锁钱包)：

```
new >>> set_password my_password
```

执行成功后会显示:
```
locked >>>
```

解锁钱包:
```
locked >>> unlock my_password
```

解锁成功会显示：
```
unlocked >>>
```

使用 info 命令可以查看当前区块同步情况
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


## jsonrpc 调用示例

进入命令行（cmd），通过curl进行调用

```
curl --data '{"jsonrpc": "2.0", "method": "info", "params": [], "id": 1}' http://127.0.0.1:38091
```

即可看到返回结果

### POST请求示例

请求URL如下

```
http://127.0.0.1:38091
```

请求主体

```
{"jsonrpc": "2.0", "method": "info", "params": [], "id": 1}
```

注：params的格式为`[API类型，API指令，参数]`


返回结果

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
