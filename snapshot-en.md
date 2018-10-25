### Save the snapshot of data storage in witness_node

#### Download the newest version of witness_node program, downloading address

**The program might be updated, please**[**click here**](https://github.com/dbxone/dbxchain/releases/latest)**download the newest program**

| :--- | :--- |
| github | [https://github.com/dbxone/dbxchain/releases/download/1.0.180604/dbx_1.0.180604.tar.gz](https://github.com/dbxone/dbxchain/releases/download/1.0.180604/dbx_1.0.180604.tar.gz) |

#### Start witness_node program, designate the block height and snapshot file path in the initiating parameter

```
./programs/witness_node/witness_node --data-dir=trusted_node \
--rpc-endpoint="0.0.0.0:38090" --p2p-endpoint="0.0.0.0:38091" \
 --log-file --max-ops-per-account=0 --partial-operations=true \
 --data-transaction-lifetime=1 \
 --plugins snapshot \
 --snapshot-at-block 9623000 --snapshot-to snapshot.0604.txt &
```

Thereinto--snapshot-at-block 9623000 designates the block height, namely saving the snapshot at this height; --snapshot-to snapshot.0604.txt designates the snapshot files, saved in the current directory\(can also use the absolute path\)

If the designated block height is smaller than the newest block height, namely the snapshot at certain past time, it is needed to add--replay-blockchain parameter when you start witness_node

#### All the RAM data objects will be saved in the snapshot file in lines, every line is a json. See the following：

```
{"id":"1.2.0","membership_expiration_date":"2106-02-07T06:28:15","merchant_expiration_date":"1970-01-01T00:00:00","datasource_expiration_date":"1970-01-01T00:00:00","data_transaction_member_expiration_date":"1970-01-01T00:00:00","registrar":"1.2.0","referrer":"1.2.0","lifetime_referrer":"1.2.0","merchant_auth_referrer":"1.2.0","datasource_auth_referrer":"1.2.0","network_fee_percentage":2000,"lifetime_referrer_fee_percentage":8000,"referrer_rewards_percentage":0,"name":"committee-account","owner":{"weight_threshold":1,"account_auths":[],"key_auths":[],"address_auths":[]},"active":{"weight_threshold":23858,"account_auths":[["1.2.6",45685],["1.2.7",203],["1.2.8",203],["1.2.9",203],["1.2.10",203],["1.2.11",203],["1.2.12",203],["1.2.13",203],["1.2.14",203],["1.2.15",203],["1.2.16",203]],"key_auths":[],"address_auths":[]},"options":{"memo_key":"DBX1111111111111111111111111111111114T1Anm","voting_account":"1.2.5","num_witness":0,"num_committee":0,"votes":[],"extensions":[]},"statistics":"2.6.0","whitelisting_accounts":[],"blacklisting_accounts":[],"whitelisted_accounts":[],"blacklisted_accounts":[],"owner_special_authority":[0,{}],"active_special_authority":[0,{}],"top_n_control_flags":0}
{"id":"1.2.1","membership_expiration_date":"2106-02-07T06:28:15","merchant_expiration_date":"1970-01-01T00:00:00","datasource_expiration_date":"1970-01-01T00:00:00","data_transaction_member_expiration_date":"1970-01-01T00:00:00","registrar":"1.2.1","referrer":"1.2.1","lifetime_referrer":"1.2.1","merchant_auth_referrer":"1.2.0","datasource_auth_referrer":"1.2.0","network_fee_percentage":2000,"lifetime_referrer_fee_percentage":8000,"referrer_rewards_percentage":0,"name":"witness-account","owner":{"weight_threshold":1,"account_auths":[],"key_auths":[],"address_auths":[]},"active":{"weight_threshold":251270,"account_auths":[["1.2.6",45685],["1.2.7",45689],["1.2.8",45685],["1.2.9",45685],["1.2.10",45685],["1.2.11",45685],["1.2.12",45685],["1.2.13",45685],["1.2.14",45685],["1.2.15",45685],["1.2.16",45685]],"key_auths":[],"address_auths":[]},"options":{"memo_key":"DBX1111111111111111111111111111111114T1Anm","voting_account":"1.2.5","num_witness":0,"num_committee":0,"votes":[],"extensions":[]},"statistics":"2.6.1","whitelisting_accounts":[],"blacklisting_accounts":[],"whitelisted_accounts":[],"blacklisted_accounts":[],"owner_special_authority":[0,{}],"active_special_authority":[0,{}],"top_n_control_flags":0}
{"id":"1.2.2","membership_expiration_date":"2106-02-07T06:28:15","merchant_expiration_date":"1970-01-01T00:00:00","datasource_expiration_date":"1970-01-01T00:00:00","data_transaction_member_expiration_date":"1970-01-01T00:00:00","registrar":"1.2.2","referrer":"1.2.2","lifetime_referrer":"1.2.2","merchant_auth_referrer":"1.2.0","datasource_auth_referrer":"1.2.0","network_fee_percentage":2000,"lifetime_referrer_fee_percentage":8000,"referrer_rewards_percentage":0,"name":"relaxed-committee-account","owner":{"weight_threshold":1,"account_auths":[],"key_auths":[],"address_auths":[]},"active":{"weight_threshold":23858,"account_auths":[["1.2.6",45685],["1.2.7",203],["1.2.8",203],["1.2.9",203],["1.2.10",203],["1.2.11",203],["1.2.12",203],["1.2.13",203],["1.2.14",203],["1.2.15",203],["1.2.16",203]],"key_auths":[],"address_auths":[]},"options":{"memo_key":"DBX1111111111111111111111111111111114T1Anm","voting_account":"1.2.5","num_witness":0,"num_committee":0,"votes":[],"extensions":[]},"statistics":"2.6.2","whitelisting_accounts":[],"blacklisting_accounts":[],"whitelisted_accounts":[],"blacklisted_accounts":[],"owner_special_authority":[0,{}],"active_special_authority":[0,{}],"top_n_control_flags":0}
...
{"id":"2.13.37553","time":"2018-06-04T06:00:00","record":{"time_since_last_budget":600,"from_initial_reserve":"10193891740740","from_accumulated_fees":0,"from_unused_witness_budget":300000,"requested_witness_budget":20000000,"total_budget":24209195,"witness_budget":20000000,"worker_budget":4209195,"leftover_worker_funds":4209195,"supply_delta":19700000}}
{"id":"2.13.37554","time":"2018-06-04T06:10:00","record":{"time_since_last_budget":600,"from_initial_reserve":"10193872040740","from_accumulated_fees":0,"from_unused_witness_budget":300000,"requested_witness_budget":20000000,"total_budget":24209148,"witness_budget":20000000,"worker_budget":4209148,"leftover_worker_funds":4209148,"supply_delta":19700000}}
{"id":"2.13.37555","time":"2018-06-04T06:20:00","record":{"time_since_last_budget":600,"from_initial_reserve":"10193852340740","from_accumulated_fees":0,"from_unused_witness_budget":300000,"requested_witness_budget":20000000,"total_budget":24209101,"witness_budget":20000000,"worker_budget":4209101,"leftover_worker_funds":4209101,"supply_delta":19700000}}
...
{"id":"1.25.1","owner":"1.2.15","create_date_time":"2017-10-31T14:16:16","lock_days":90,"program_id":"3","amount":{"amount":10000000,"asset_id":"1.3.1"},"interest_rate":400,"memo":""}
{"id":"1.25.3","owner":"1.2.15","create_date_time":"2017-10-31T14:16:27","lock_days":1,"program_id":"1","amount":{"amount":10000000,"asset_id":"1.3.1"},"interest_rate":400,"memo":""}
{"id":"1.25.17","owner":"1.2.17","create_date_time":"2017-10-31T14:18:22","lock_days":1,"program_id":"1","amount":{"amount":500000,"asset_id":"1.3.1"},"interest_rate":400,"memo":""}
...
{"id":"2.5.0","owner":"1.2.0","asset_type":"1.3.0","balance":"1982649276131"}
{"id":"2.5.1","owner":"1.2.17","asset_type":"1.3.0","balance":"99975815407107840"}
{"id":"2.5.2","owner":"1.2.18","asset_type":"1.3.0","balance":"100275999963"}
{"id":"2.5.3","owner":"1.2.6","asset_type":"1.3.0","balance":75234770}
{"id":"2.5.4","owner":"1.2.7","asset_type":"1.3.0","balance":"9921797683209"}
{"id":"2.5.5","owner":"1.2.8","asset_type":"1.3.0","balance":"49990752447"}
...
{"id":"2.16.0","accumulated_fba_fees":0,"designated_asset":"1.3.743"}
{"id":"2.16.1","accumulated_fba_fees":0,"designated_asset":"1.3.743"}
{"id":"2.16.2","accumulated_fba_fees":0,"designated_asset":"1.3.743"}
```

Among the above json files, every line is a json, among which id is the object id, 1.25.x is the loyalty plan balance object, 2.5.x is the balance object; Refer to [here](https://github.com/dbxone/dbxchain/wiki/Objects-and-IDS) for object ID files

If you want to parse DBX balance of the account, you need to parse 1.25.x and 2.5.x, and 1.3.1 of the asset_id, owner as the account the balance belongs to.
