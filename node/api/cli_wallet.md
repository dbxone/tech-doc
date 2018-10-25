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

进行api调用前，请详读[api rpc格式](format.md)

```
cli_wallet -w wallet.json -s ws://<ip>:<port1> -r <ip>:<port2> -H <ip>:<port3> --chain-id <...>
```

* `-r <ip>:<port2>` 对外提供钱包rpc api服务，包括http和websocket服务。
* `-H <ip>:<port3>` 对外提供钱包rpc api服务，它只包含http服务，跟<port2>的区别在于，对于它的返回值是http格式的json格式，其它都相同。






### <port2> http+rpc

进入命令行，通过curl进行post请求调用

```
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":[0,"api指令",[参数]]}'
或
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"api指令","params":[参数]}'
```
即可看到返回结果。


<b>具体请求URL为</b>

`http://<ip>:<port2>`


eg.
```
获取api帮助信息
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"help","params": []}'
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":[0,"help",[]]}'

解锁服务钱包
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"unlock","params": ["mypassword"]}'
curl http://127.0.0.1:38091 -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":[0,"unlock",["mypassword"]]}'

转账
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"transfer","params": ["user1","user2","1","DBX","memo", true]}'
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":[0,"transfer",["user1","user2","1","DBX","memo", true]]}'

生成公私钥
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"suggest_brain_key","params": []}'
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":[0,"suggest_brain_key",[]}'

注册账户
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"register_account","params": ["userx","pubkey","pubkey","root","root", 0, true]}'
curl http://<ip>:<port2> -H "Content-Type:application/json" -X POST -d '{"id":1,"method":"call","params":[0,"register_account",["userx","pubkey","pubkey","root","root", 0, true]]}'
```







### <port2> websocket+rpc

进入命令行，通过wscat进行请求调用，wscat安装方式`apt -y install node-ws`。

```
wscat -c ws://<ip>:<port2>
```


<b>具体请求URL为</b>

`ws://<ip>:<port2>`



eg.
```
获取api帮助信息
{"id":1,"method":"help","params": []}
{"id":1,"method":"call","params":[0,"help",[]]}

解锁服务钱包
{"id":1,"method":"unlock","params": ["mypassword"]}
{"id":1,"method":"call","params":[0,"unlock",["mypassword"]]}

转账
{"id":1,"method":"transfer","params": ["user1","user2","1","DBX","memo", true]}
{"id":1,"method":"call","params":[0,"transfer",["user1","user2","1","DBX","memo", true]]}

生成公私钥
{"id":1,"method":"suggest_brain_key","params": []}
{"id":1,"method":"call","params":[0,"suggest_brain_key",[]}

注册账户
{"id":1,"method":"register_account","params": ["userx","pubkey","pubkey","root","root", 0, true]}
{"id":1,"method":"call","params":[0,"register_account",["userx","pubkey","pubkey","root","root", 0, true]]}
```
