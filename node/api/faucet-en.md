# Faucet api

There is only one faucet api, which is the one used in registrating the account.

The faucet service port is `<ip>:<port4>`。

Enter the command line, execute post request call by curl

```
curl http://<ip>:<port4>/api/v1/accounts -H "Content-Type:application/json" -X POST -d 'calling subject'
```
you will see the calling result.


<b> detialed requested URL is </b>

`http://<ip>:<port4>/api/v1/accounts`


<b> calling subject is in format </b>

```
{
    "account":{
        "name":"<username>",              #Newly registered account
        "owner_key":"<public key1>",      #Owner's public key of the account
        "active_key":"<public key2>",     #Active public key
        "memo_key":"<public key2>",       #Memo public key, which is the same to the active public key
        "refcode":null,                   #Parent id, which is null
        "referrer":null
    }				
}
```

<b> return successfully </b>
```
{
    "account":{
        "id":null,                        #The returned user id is null here
        "name":"<username>",
        "owner_key":"<public key1>",
        "active_key":"<public key2>"
    }
}
```

<b> fails to return </b>
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
