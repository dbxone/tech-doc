# 简要python账户注册代码示例

本程序，先调用钱包api生成公私钥，然后调用水龙头api注册账户。

```
import os
import requests
import json


# 调用钱包api，获取公私钥
url = "http://127.0.0.1:38091"
payload = "{\"id\":1,\"method\":\"suggest_brain_key\",\"params\": []}"
headers = {
    'Content-Type': "application/json",
    }

response = requests.request("POST", url, data=payload, headers=headers)

print response.text, type(response.text)
print



# 解析出公斯钥
j=response.json()
print j, type(j)
print

result=j["result"]

print result["brain_priv_key"]
print result["pub_key"]
print result["wif_priv_key"]




# 调用水龙头api，进行账户注册
url = "http://13.57.136.245:3000/api/v1/accounts"

payload = "{\"account\":{\"name\":\"mytestuser8\",\"owner_key\":\"" + result["pub_key"] + "\",\"active_key\":\"" + result["pub_key"] + "\",\"memo_key\":\"" + result["pub_key"] + "\",\"refcode\":null,\"referrer\":null}}"

print payload, type(payload)
headers = {
    'Content-Type': "application/json"
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```