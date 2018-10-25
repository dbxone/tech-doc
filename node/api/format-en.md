# api rpc format

All the rpc calling of DBXChainc api is in jsonrpc2.0 standard format, please refer to [jsonrpc2.0.pdf](jsonrpc2.0.pdf) for the jsonrpc2.0 standard format.

## 1. There are two formats for the calling subject

* Direct calling format
```
{"id":1,"method":"api instruction","params":[Parameter]}
```

* call calling format

```
{"id":1,"method":"call","params":[api type value,"api instruction",[Parameter]]}
or
{"id":1,"method":"call","params":["api type string","api instruction",[Parameter]]}
```

Thereinto
```
{"id":1,"method":"call","params":[0,"api instruction",[Parameter]]}
equal to 
{"id":1,"method":"api instruction","params":[Parameter]}
```


## 2. Two formats of the return value
<b> The return can be `jsonrpc2.0 format` or `jsonrpc2.0 format in http format`</b> bassed on different service types.

Compared to `jsonrpc2.0 format`, `jsonrpc2.0 format in http format` directly add `\` to the controlling character in the returning result.

* Successful return

```
{"id":1,"jsonrpc":"2.0","result":null}
```
or
```
{"id":1,"jsonrpc":"2.0","result":{...}}
```

* Failed return
```
{"id":1,"jsonrpc":"2.0","error":{...}}
```
