# 水龙头 api

水龙头api只有一个，就是注册账号使用的api。

水龙头服务接口为 `<ip>:<port4>`。

进入命令行，通过curl进行post请求调用

```
curl http://<ip>:<port4>/api/v1/accounts -H "Content-Type:application/json" -X POST -d '调用主体'
```
即可看到返回结果。


<b>具体请求URL为</b>

`http://<ip>:<port4>/api/v1/accounts`


<b>调用主体格式为</b>

```
{
    "account":{
        "name":"<username>",              #新注册的用户名
        "owner_key":"<public key1>",      #所有者账户公钥
        "active_key":"<public key2>",     #活跃公钥
        "memo_key":"<public key2>",       #备忘公钥，与活跃公钥相同
        "refcode":null,                   #父账户的id，为null即可
        "referrer":null
    }				
}
```

<b>正确返回</b>
```
{
    "account":{
        "id":null,                        #此处返回的用户id为null
        "name":"<username>",
        "owner_key":"<public key1>",
        "active_key":"<public key2>"
    }
}
```

<b>失败返回</b>
```
{
    "error":{
        ...
    }
}
```


eg. 
```
curl http://<ip>:<port4>/api/v1/accounts -H "Content-Type:application/json" -X POST -d '{"account":{"name":"mytestuser","owner_key":"DBX8ahfEujigjL8CcU26wJeqnDqGjumLneE31CShLimBAfWbcHFtS","active_key":"DBX5mJSXTdWs7qFuYTZCUJPrhiasgQatXx8LKxD6jHQXw6NL8h6rc","memo_key":"DBX5mJSXTdWs7qFuYTZCUJPrhiasgQatXx8LKxD6jHQXw6NL8h6rc","refcode":null,"referrer":null}}'
```