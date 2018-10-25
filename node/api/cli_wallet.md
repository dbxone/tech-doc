# 钱包 api


## 钱包api

| 命令 | 参数 | 参数 | 说明 |
| :--- | :--- | :--- | :--- |
| [set_password](cli_wallet/setpassword.md) | &lt;new_password&gt; | 对钱包设置一个新密码。首次启动钱包，需要设置密码 |  |
| [unlock](cli_wallet/unlock.md) | &lt;my_password&gt; | 解锁钱包 |  |
| [import_key](cli_wallet/importkey.md) | &lt;account_name_or_id&gt;         &lt;true&gt; &lt;wif_private_key&gt; | 将帐户的私钥导入到钱包 |  |
| [dump_private_keys](cli_wallet/dumpprivate-keys.md) |  | 打印钱包拥有的所有私钥对 |  |
| [info](cli_wallet/getaccount.md) | &lt;account_name_or_id&gt; | 查询指定帐户信息，参数可以为帐户名或者帐户id |  |
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

## 2. 访问方式

```
cli_wallet -w wallet.json -s ws://<ip>:<port1> -r <ip>:<port2> -H <ip>:<port3> --chain-id <...>
```

* `-r <ip>:<port2>` 对外提供钱包rpc api服务，包括http和websocket服务。
* `-H <ip>:<port3>` 对外提供rpc api服务，它只包含http服务，跟<port2>的区别在于，对于它的返回值是http格式的json格式，其它都相同。


### <port2> http+rpc

jsonrpc2.0标准请查阅[jsonrpc2.0.pdf](jsonrpc2.0.pdf)

进入命令行，通过curl进行post请求调用

```
curl http://<ip>:<port1>/rpc -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":[api类型值,"api指令",[参数]]}'
或
curl http://<ip>:<port1>/rpc -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":["api类型串","api指令",[参数]]}'
```
即可看到返回结果。


进入命令行，通过curl进行调用

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
