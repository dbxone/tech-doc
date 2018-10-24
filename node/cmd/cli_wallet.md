# cli_wallet 启动参数

| *参数 | 说明* |
|:--- |:--- |
| -h [ --help ] | Print this help message and exit. <br> 帮助信息 |
| -s [ --server-rpc-endpoint ] [=arg(=ws://127.0.0.1:8090)] | Server websocket RPC endpoint <br> 连接witness_node的websocket接口 |
| -u [ --server-rpc-user ] arg | Server Username <br> 登陆钱包的用户名 |
| -p [ --server-rpc-password ] arg | Server Password <br> 登陆钱包的密码 |
| -r [ --rpc-endpoint ] [=arg(=127.0.0.1:8091)] | Endpoint for wallet websocket RPC to listen on <br> 提供wallet websocket的服务接口 |
| -t [ --rpc-tls-endpoint ] [=arg(=127.0.0.1:8092)] | Endpoint for wallet websocket TLS RPC to listen on <br> 提供wallet服务的tls接口 |
| -c [ --rpc-tls-certificate ] [=arg(=server.pem)] | PEM certificate for wallet websocket TLS RPC <br> 提供wallet服务的tls证书 |
| -H [ --rpc-http-endpoint ] [=arg(=127.0.0.1:8093)] | Endpoint for wallet HTTP RPC to listen on <br> 提供wallet http的服务接口 |
| -d [ --daemon ] | Run the wallet in daemon mode <br> 守候服务 |
| -w [ --wallet-file ] [=arg(=wallet.json)] | wallet to load <br> 指定的钱包文件 |
| --chain-id arg | chain ID to connect to <br> 连接的链id |
| -v [ --version ] | Display version information <br> 查看版本信息 |

# 使用示例


# cli_wallet退出
witness_node重启以后，需要重新启动cli_wallet。

因为cli_wallet后台运行时，不会自动退出。

关闭cli_wallet的方法 : `kill -s SIGINT $(pgrep cli_wallet)`