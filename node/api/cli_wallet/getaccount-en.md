# get_account

##### Explanation：Query information about the designated account, parameter can b account name or id

##### usage: get_account account_name_or_id

##### Parameter: account_name_or_id

| Parameter | Explanation |
| :--- | :--- |
| account_name_or_id | Account name or id |

### 

### **Calling case**

#### CURL  POST command line request
Enter the command line进入命令行, input

```
curl --data '{"jsonrpc": "2.0", "method": "call", "params": [0, "get_accounts", [["1.2.1","1.2.2"]]], "id": 1}'  https://node1.dbx.io/rpc
```

The return is shown



#### POST request case

Request URL as follows

```
https://node1.dbx.io/
```

Requesting subjective

```
{
"jsonrpc": "2.0", 
"method": "call", 
"params": [0, "get_accounts", [["1.2.1","1.2.2"]]], "id": 1
}
```

Return

```
{
    "id":1,
    "jsonrpc":"2.0",
    "result":[
        {
            "id":"1.2.1",
            "membership_expiration_date":"1969-12-31T23:59:59",
            "merchant_expiration_date":"1970-01-01T00:00:00",
            "datasource_expiration_date":"1970-01-01T00:00:00",
            "data_transaction_member_expiration_date":"1970-01-01T00:00:00",
            "registrar":"1.2.1",
            "referrer":"1.2.1",
            "lifetime_referrer":"1.2.1",
            "merchant_auth_referrer":"1.2.0",
            "datasource_auth_referrer":"1.2.0",
            "network_fee_percentage":2000,
            "lifetime_referrer_fee_percentage":8000,
            "referrer_rewards_percentage":0,
            "name":"witness-account",
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
                "weight_threshold":391175,
                "account_auths":[
                    [
                        "1.2.18",
                        37288
                    ],
                    [
                        "1.2.19",
                        37253
                    ],
                    [
                        "1.2.20",
                        37253
                    ],
                    [
                        "1.2.21",
                        37253
                    ],
                    [
                        "1.2.22",
                        37253
                    ],
                    [
                        "1.2.29",
                        37253
                    ],
                    [
                        "1.2.30",
                        37253
                    ],
                    [
                        "1.2.31",
                        37253
                    ],
                    [
                        "1.2.32",
                        37253
                    ],
                    [
                        "1.2.33",
                        37253
                    ],
                    [
                        "1.2.34",
                        37253
                    ],
                    [
                        "1.2.35",
                        37253
                    ],
                    [
                        "1.2.36",
                        37253
                    ],
                    [
                        "1.2.37",
                        37253
                    ],
                    [
                        "1.2.38",
                        37253
                    ],
                    [
                        "1.2.39",
                        37253
                    ],
                    [
                        "1.2.3429",
                        37253
                    ],
                    [
                        "1.2.3431",
                        37253
                    ],
                    [
                        "1.2.3432",
                        37253
                    ],
                    [
                        "1.2.3433",
                        37253
                    ],
                    [
                        "1.2.3434",
                        37253
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
            "statistics":"2.6.1",
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
        },
        {
            "id":"1.2.2",
            "membership_expiration_date":"1969-12-31T23:59:59",
            "merchant_expiration_date":"1970-01-01T00:00:00",
            "datasource_expiration_date":"1970-01-01T00:00:00",
            "data_transaction_member_expiration_date":"1970-01-01T00:00:00",
            "registrar":"1.2.2",
            "referrer":"1.2.2",
            "lifetime_referrer":"1.2.2",
            "merchant_auth_referrer":"1.2.0",
            "datasource_auth_referrer":"1.2.0",
            "network_fee_percentage":2000,
            "lifetime_referrer_fee_percentage":8000,
            "referrer_rewards_percentage":0,
            "name":"relaxed-committee-account",
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
                "weight_threshold":204892,
                "account_auths":[
                    [
                        "1.2.18",
                        37253
                    ],
                    [
                        "1.2.19",
                        37253
                    ],
                    [
                        "1.2.20",
                        37253
                    ],
                    [
                        "1.2.21",
                        37253
                    ],
                    [
                        "1.2.22",
                        37253
                    ],
                    [
                        "1.2.23",
                        37253
                    ],
                    [
                        "1.2.24",
                        37253
                    ],
                    [
                        "1.2.25",
                        37253
                    ],
                    [
                        "1.2.26",
                        37253
                    ],
                    [
                        "1.2.27",
                        37253
                    ],
                    [
                        "1.2.28",
                        37253
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
            "statistics":"2.6.2",
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
    ]
}
```
