# cli_wallet Initiating parameter

| *Parameter | Explanation* |
|:--- |:--- |
| -h [ --help ] | Print this help message and exit. <br> help message |
| -s [ --server-rpc-endpoint ] [=arg(=ws://127.0.0.1:8090)] | Server websocket RPC endpoint <br> connect to the websocket interface of the witness_node |
| -u [ --server-rpc-user ] arg | Server Username <br> Log in with the wallet username |
| -p [ --server-rpc-password ] arg | Server Password <br> Log in with the wallet password |
| -r [ --rpc-endpoint ] [=arg(=127.0.0.1:8091)] | Endpoint for wallet websocket RPC to listen on <br> Offer the service interface of the wallet websocket |
| -t [ --rpc-tls-endpoint ] [=arg(=127.0.0.1:8092)] | Endpoint for wallet websocket TLS RPC to listen on <br> Offer the tls interface of the wallet service|
| -c [ --rpc-tls-certificate ] [=arg(=server.pem)] | PEM certificate for wallet websocket TLS RPC <br> Offer the tls certificate of the wallet service |
| -H [ --rpc-http-endpoint ] [=arg(=127.0.0.1:8093)] | Endpoint for wallet HTTP RPC to listen on <br> Offer the service interface of wallet http |
| -d [ --daemon ] | Run the wallet in daemon mode <br> Waiting service |
| -w [ --wallet-file ] [=arg(=wallet.json)] | wallet to load <br> Designated wallet file |
| --chain-id arg | chain ID to connect to <br> Connected chain id |
| -v [ --version ] | Display version information <br> Find the version information |

# Usage case
Command line wallet cli_wallet connects to switness_node:
```
cli_wallet -w wallet.json -s ws://127.0.0.1:38090 -r 127.0.0.1:38091 -H 127.0.0.1:38092 --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d
```

* `-w wallet.json` Designate the wallet file
* `-s ws://127.0.0.1:38090`  Connected witness_node
* `-r 127.0.0.1:38091` Provide wallet rpc api service to the public，including jsonrpc and websocket service，please refer to [api calling logic] for more details (../api/introduction.md)
* `-H 127.0.0.1:38092` Provide http jsonrpc api service to the public，please refer to [api calling logic] for more details (../api/introduction.md)
* --chain-id 6e340b9cffb37a989ca544e6bb780a2c78901d3fb33738768511a30617afa01d Connected chain id


# cli_wallet Exit
After restarting witness_node, cli_wallet needs to be restarted.

It will not automatically exit when cli_wallet is running at the back desk.

Method to close cli_wallet: `kill -s SIGINT $(pgrep cli_wallet)`
