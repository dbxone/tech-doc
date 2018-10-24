# cli_wallet 命令列表

| 命令 | 参数 | 说明 | 备注 |
| :--- | :--- | :--- | :--- |
| [set_password](cli_wallet/setpassword.md) | &lt;new_password&gt; | 对钱包设置一个新密码。首次启动钱包，需要设置密码 |  |
| [unlock](cli_wallet/unlock.md) | &lt;my_password&gt; | 解锁钱包 |  |
| [import_key](cli_wallet/importkey.md) | &lt;account_name_or_id&gt;         &lt;true&gt; &lt;wif_private_key&gt; | 将帐户的私钥导入到钱包 |  |
| [dump_private_keys](cli_wallet/dumpprivate-keys.md) |  | 打印钱包拥有的所有私钥对 |  |
| [get_account](cli_wallet/getaccount.md) | &lt;account_name_or_id&gt; | 查询指定帐户信息，参数可以为帐户名或者帐户id |  |
| [list_account_balances](cli_wallet/listaccount-balances.md) | &lt;account_name_or_id&gt; | 查询帐户余额 |  |
| [get_account_history](cli_wallet/getaccount-history.md) | &lt;account_name_or_id&gt;         &lt;limt_num&gt; | 查询帐户最近的交易记录 |  |
| [get_relative_account_history](cli_wallet/getrelative-account-history.md) | &lt;account_name_or_id&gt;       &lt;start&gt; &lt;limit&gt; &lt;stop&gt; | 查询帐户最近的交易记录, 支持翻页 |  |
| [get_account_history_by_operations](cli_wallet/getrelative-account-history_by_operations.md) | &lt;account_name_or_id&gt; &lt;\[\]&gt;  &lt;start&gt; &lt;limit_num&gt; | 根据oeration_type查询帐户最近的交易记录，并且返回 operation对应的txID |  |
| [transfer](cli_wallet/transfer.md) | &lt;from_account&gt;                   &lt;to_account&gt; &lt;amount&gt;     &lt;DBX&gt; &lt;memo&gt; &lt;true&gt; | 转帐操作 |  |
| [transfer2](cli_wallet/transfer2.md) | &lt;from_account&gt;                   &lt;to_account&gt; &lt;amount&gt;     &lt;DBX&gt; &lt;memo&gt; &lt;true&gt; | 转帐操作，参数同transfer, 返回结果中包含当前交易的id |  |
| [get_block](cli_wallet/getblock.md) | &lt;block_num&gt; | 获取指定区块信息 |  |
| [info](cli_wallet/info.md) |  | 获取区块链信息，可以用此命令查询最新区块高度 |  |
| [help](cli_wallet/help.md) |  | 帮助命令，此命令会返回钱包支持的所有接口 |  |
| [gethelp](cli_wallet/gethelp.md) | &lt;command&gt; | 帮助命令，查看指定钱包命令的调用方法 |  |

## **调用示例**

命令行钱包cli_wallet连接witness_node:
```
./programs/cli_wallet/cli_wallet --data-dir=trusted_node -s ws://127.0.0.1:38090 -r 127.0.0.1:38091 
```
首先需要为钱包设置一个钱包密码(这个密码是本地的，用来解锁钱包)：

new >>> set_password my_password

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
  "head_block_num": 3913758,
  "head_block_id": "003bb81eec2abfdb2cf58ffdf4dd547ea190530e",
  "head_block_age": "3 seconds old",  # head_block_age表示最新的区块时间，系统每3秒出一块
  "next_maintenance_time": "0 second ago",
  "chain_id": "4f7d07969c446f8342033acb3ab2ae5044cbe0fde93db02de75bd17fa8fd84b8",
  "participation": "100.00000000000000000",
  ...
 }
 ```
 

## jsonrpc 调用示例

以get_account为例

### CURL POST 命令行请求

进入命令行（cmd），输入

```
curl --data '{"jsonrpc": "2.0", "method": "get_account", "params": ["nathan"], "id": 1}' http://127.0.0.1:38091
```

即可看到返回结果

#### POST请求示例

请求URL如下

```
http://127.0.0.1:38091
```

请求主体

```
{"jsonrpc": "2.0", "method": "get_account", "params": ["nathan"], "id": 1}
```

注：params的格式为\[API类型，API指令，参数\]


返回结果

```
{
    "id":1,
    "jsonrpc":"2.0",
    "result":[
        {
            "id":"1.2.1",
            "membership_expiration_date":"1969-12-31T23:59:59",
            "merchant_expiration_date":"1970-01-01T00:00:00",
            "datasource_expiration_date":"1970-01-01T00:00:00",
            "data_transaction_member_expiration_date":"1970-01-01T00:00:00",
            "registrar":"1.2.1",
            "referrer":"1.2.1",
            "lifetime_referrer":"1.2.1",
            "merchant_auth_referrer":"1.2.0",
            "datasource_auth_referrer":"1.2.0",
            "network_fee_percentage":2000,
            "lifetime_referrer_fee_percentage":8000,
            "referrer_rewards_percentage":0,
            "name":"witness-account",
            "owner":{
                "weight_threshold":1,
                "account_auths":[

                ],
                "key_auths":[

                ],
                "address_auths":[

                ]
            },
            "active":{
                "weight_threshold":391175,
                "account_auths":[
                    [
                        "1.2.18",
                        37288
                    ],
                    [
                        "1.2.19",
                        37253
                    ],
                    [
                        "1.2.20",
                        37253
                    ],
                    [
                        "1.2.21",
                        37253
                    ],
                    [
                        "1.2.22",
                        37253
                    ],
                    [
                        "1.2.29",
                        37253
                    ],
                    [
                        "1.2.30",
                        37253
                    ],
                    [
                        "1.2.31",
                        37253
                    ],
                    [
                        "1.2.32",
                        37253
                    ],
                    [
                        "1.2.33",
                        37253
                    ],
                    [
                        "1.2.34",
                        37253
                    ],
                    [
                        "1.2.35",
                        37253
                    ],
                    [
                        "1.2.36",
                        37253
                    ],
                    [
                        "1.2.37",
                        37253
                    ],
                    [
                        "1.2.38",
                        37253
                    ],
                    [
                        "1.2.39",
                        37253
                    ],
                    [
                        "1.2.3429",
                        37253
                    ],
                    [
                        "1.2.3431",
                        37253
                    ],
                    [
                        "1.2.3432",
                        37253
                    ],
                    [
                        "1.2.3433",
                        37253
                    ],
                    [
                        "1.2.3434",
                        37253
                    ]
                ],
                "key_auths":[

                ],
                "address_auths":[

                ]
            },
            "options":{
                "memo_key":"DBX1111111111111111111111111111111114T1Anm",
                "voting_account":"1.2.5",
                "num_witness":0,
                "num_committee":0,
                "votes":[

                ],
                "extensions":[

                ]
            },
            "statistics":"2.6.1",
            "whitelisting_accounts":[

            ],
            "blacklisting_accounts":[

            ],
            "whitelisted_accounts":[

            ],
            "blacklisted_accounts":[

            ],
            "owner_special_authority":[
                0,
                {

                }
            ],
            "active_special_authority":[
                0,
                {

                }
            ],
            "top_n_control_flags":0
        },
        {
            "id":"1.2.2",
            "membership_expiration_date":"1969-12-31T23:59:59",
            "merchant_expiration_date":"1970-01-01T00:00:00",
            "datasource_expiration_date":"1970-01-01T00:00:00",
            "data_transaction_member_expiration_date":"1970-01-01T00:00:00",
            "registrar":"1.2.2",
            "referrer":"1.2.2",
            "lifetime_referrer":"1.2.2",
            "merchant_auth_referrer":"1.2.0",
            "datasource_auth_referrer":"1.2.0",
            "network_fee_percentage":2000,
            "lifetime_referrer_fee_percentage":8000,
            "referrer_rewards_percentage":0,
            "name":"relaxed-committee-account",
            "owner":{
                "weight_threshold":1,
                "account_auths":[

                ],
                "key_auths":[

                ],
                "address_auths":[

                ]
            },
            "active":{
                "weight_threshold":204892,
                "account_auths":[
                    [
                        "1.2.18",
                        37253
                    ],
                    [
                        "1.2.19",
                        37253
                    ],
                    [
                        "1.2.20",
                        37253
                    ],
                    [
                        "1.2.21",
                        37253
                    ],
                    [
                        "1.2.22",
                        37253
                    ],
                    [
                        "1.2.23",
                        37253
                    ],
                    [
                        "1.2.24",
                        37253
                    ],
                    [
                        "1.2.25",
                        37253
                    ],
                    [
                        "1.2.26",
                        37253
                    ],
                    [
                        "1.2.27",
                        37253
                    ],
                    [
                        "1.2.28",
                        37253
                    ]
                ],
                "key_auths":[

                ],
                "address_auths":[

                ]
            },
            "options":{
                "memo_key":"DBX1111111111111111111111111111111114T1Anm",
                "voting_account":"1.2.5",
                "num_witness":0,
                "num_committee":0,
                "votes":[

                ],
                "extensions":[

                ]
            },
            "statistics":"2.6.2",
            "whitelisting_accounts":[

            ],
            "blacklisting_accounts":[

            ],
            "whitelisted_accounts":[

            ],
            "blacklisted_accounts":[

            ],
            "owner_special_authority":[
                0,
                {

                }
            ],
            "active_special_authority":[
                0,
                {

                }
            ],
            "top_n_control_flags":0
        }
    ]
}
```
