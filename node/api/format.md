# api rpc 格式

DBXChain所有api的rpc调用都采用通用的jsonrpc2.0标准格式，jsonrpc2.0标准请查阅[jsonrpc2.0.pdf](jsonrpc2.0.pdf)。

## 1. 调用主体有两种格式

* 直接调用格式
```
{"id":1,"method":"api指令","params":[参数]}
```

* call调用格式

```
{"id":1,"method":"call","params":[api类型值,"api指令",[参数]]}
或
{"id":1,"method":"call","params":["api类型字串","api指令",[参数]]}
```

其中
```
{"id":1,"method":"call","params":[0,"api指令",[参数]]}
等同于
{"id":1,"method":"api指令","params":[参数]}
```


## 2. 返回值两种格式
<b>根据服务类型的不同，返回结果为`jsonrpc2.0格式` 或 `http格式的jsonrpc2.0格式`</b>

`http格式的jsonrpc2.0格式`相比较`jsonrpc2.0格式`，直接把返回结果中的控制字符加上`\`。

* 正确返回

```
{"id":1,"jsonrpc":"2.0","result":null}
```
或
```
{"id":1,"jsonrpc":"2.0","result":{...}}
```

* 失败返回
```
{"id":1,"jsonrpc":"2.0","error":{...}}
```