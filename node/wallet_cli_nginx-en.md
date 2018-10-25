# nginx proxy sets up cli_wallet endpoint forward

rpc service of the wallet is only accessible locally, if you need other machines to access the rpc service of the wallet，you can set up nginx proxy at the wallet nodes, restricting IP access.

### 1. Install nginx

```
cd /etc/apt/
cp sources.list sources.list.bak

echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse' > sources.list
sudo apt-get update
sudo apt-get install nginx

```

### 2. Set up nginx

Add cli_wallet.conf，located in /etc/nginx/conf.d directory，content shown as follows：

```
server { 
    listen 8888;  # Monitoring endpoint
    location / { 
        proxy_pass http://127.0.0.1:38091; 
        proxy_http_version 1.1; 

        allow 192.168.1.119;  # Accessible IP
        allow 192.168.1.118;  # Accessible IP
        deny all;             # Prohibit access by other IP
    } 
}
```

### 3. Reload the configuration

Execute the following command：

```
sudo nginx -s reload

```

### 4. Test

The configuration is completed. At this moment only two machines whose ip are 192.168.1.118 and 192.168.1.119 have the access，it will return 403 error once accessed by other IPs.

rpc address of the wallet becomes：[http://${host_ip}:8888/rpc](http://%24%7Bhost_ip%7D:8888/rpc) among which ${host_ip} is the ip of the wallet server，endpoint is 8888, nginx will send the request by the 8888 endpoint to 8091.



```
curl --data '{"jsonrpc": "2.0", "method": "get_account", "params": ["1.2.0"], "id": 2}' http://192.168.1.119:8888/rpc
```

Return as follows：

```
{
    "id":2,
    "result":{
        "id":"1.2.0",
        "membership_expiration_date":"1969-12-31T23:59:59",
        "merchant_expiration_date":"1970-01-01T00:00:00",
        "datasource_expiration_date":"1970-01-01T00:00:00",
        "data_transaction_member_expiration_date":"1970-01-01T00:00:00",
        "registrar":"1.2.0",
        "referrer":"1.2.0",
        "lifetime_referrer":"1.2.0",
        "merchant_auth_referrer":"1.2.0",
        "datasource_auth_referrer":"1.2.0",
        "network_fee_percentage":2000,
        "lifetime_referrer_fee_percentage":8000,
        "referrer_rewards_percentage":0,
        "name":"committee-account",
        "owner":{
            "weight_threshold":1,
            "account_auths":[

            ],
            "key_auths":[

            ],
            "address_auths":[

            ]
        },
        "active":{
            "weight_threshold":22743,
            "account_auths":[
                [
                    "1.2.6",
                    45474
                ],
                [
                    "1.2.7",
                    1
                ],
                [
                    "1.2.8",
                    1
                ],
                [
                    "1.2.9",
                    1
                ],
                [
                    "1.2.10",
                    1
                ],
                [
                    "1.2.11",
                    1
                ],
                [
                    "1.2.12",
                    1
                ],
                [
                    "1.2.13",
                    1
                ],
                [
                    "1.2.14",
                    1
                ],
                [
                    "1.2.15",
                    1
                ],
                [
                    "1.2.16",
                    1
                ]
            ],
            "key_auths":[

            ],
            "address_auths":[

            ]
        },
        "options":{
            "memo_key":"DBX1111111111111111111111111111111114T1Anm",
            "voting_account":"1.2.5",
            "num_witness":0,
            "num_committee":0,
            "votes":[

            ],
            "extensions":[

            ]
        },
        "statistics":"2.6.0",
        "whitelisting_accounts":[

        ],
        "blacklisting_accounts":[

        ],
        "whitelisted_accounts":[

        ],
        "blacklisted_accounts":[

        ],
        "owner_special_authority":[
            0,
            {

            }
        ],
        "active_special_authority":[
            0,
            {

            }
        ],
        "top_n_control_flags":0
    }
}
```
