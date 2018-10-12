# cli_wallet 参数使用说明

| *参数 | 说明* |
|:---: |:---: |
| -h [ --help ] | Print this help message and exit. |
| -s [ --server-rpc-endpoint ] [=arg(=ws://127.0.0.1:8090)] | Server websocket RPC endpoint |
| -u [ --server-rpc-user ] arg | Server Username |
| -p [ --server-rpc-password ] arg | Server Password |
| -r [ --rpc-endpoint ] [=arg(=127.0.0.1:8091)] | Endpoint for wallet websocket RPC to listen on |
| -t [ --rpc-tls-endpoint ] [=arg(=127.0.0.1:8092)] | Endpoint for wallet websocket TLS RPC to listen on |
| -c [ --rpc-tls-certificate ] [=arg(=server.pem)] | PEM certificate for wallet websocket TLS RPC |
| -H [ --rpc-http-endpoint ] [=arg(=127.0.0.1:8093)] | Endpoint for wallet HTTP RPC to listen on |
| -d [ --daemon ] | Run the wallet in daemon mode |
| -w [ --wallet-file ] [=arg(=wallet.json)] | wallet to load |
| --chain-id arg | chain ID to connect to |
| -v [ --version ] | Display version information |
