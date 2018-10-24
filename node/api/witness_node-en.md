## Witness API command list

### database api

| Command | Parameter | Explanation | Note |
| :--- | :--- | :--- | :--- |
| [get_objects](witness_node/getobjects.md) | &lt;ids&gt; | Find the target objective according to its ID |  |
| set_subscribe_callback | &lt;cb&gt; &lt;clear_filter&gt; | Callback for the registration of global subscription |  |
| set_data_transaction_subscribe_callback | &lt;cb&gt; &lt;clear_filter&gt; | Callback for the registration of data transaction |  |
| unsubscribe_data_transaction_callback |  | Callback for the cancellation of registrating data transaction |  |
| set_data_transaction_products_subscribe_callback | &lt;cb&gt; &lt;ids&gt; | Data transaction callback for the registration of specific data product ID |  |
| set_pending_transaction_callback | &lt;cb&gt; | Callback for the transaction whose registration has not been confirmed |  |
| set_block_applied_callback | &lt;cb&gt; | Callback for whether Set up the current block as the one registered by callback |  |
| cancel_all_subscriptions |  | Cancel all the subscriptions（callback） |  |
| [get_block_header](witness_node/getblock-header.md) | &lt;block_num&gt; | Acquire the block head information |  |
| get_transaction | &lt;block_num&gt; &lt;trx_in_block&gt; | Acquire the transaction information |  |
| get_block | &lt;block_num&gt; | Acquire the block information |  |
| get_recent_transaction_by_id | &lt;id&gt; | Query the transaction based on TXID, the return is empty if the transaction is overdue |  |
| get_chain_properties |  | Acquire the chain property |  |
| get_global_properties |  | Acquire global propoerty |  |
| get_commission_percent |  | Acquire commission ratio |  |
| get_config |  | Acquire the compiling constant |  |
| get_chain_id |  | Acquire the chain ID |  |
| get_dynamic_global_properties |  | Acquire the dynamic global property |  |
| get_key_references | &lt;key&gt; | Return all the account information pointing to the public key |  |
| is_public_key_registered | &lt;public_key&gt; | Verify whether the public key has been registered |  |
| get_accounts | &lt;account_ids&gt; | Acquire the account information by ID |  |
| [get_full_accounts](witness_node/getfullaccounts.md) | &lt;names_or_ids&gt; &lt;subscribe&gt; | Acquire all the realted information of accounts which satisfy the conditions |  |
| get_account_by_name | &lt;name&gt; | Acquire the account information by the account name |  |
| get_account_references | &lt;account_id&gt; | Acquire the account id related to account_id |  |
| lookup_account_names | &lt;account_names&gt; | Acquire the account information by the account name |  |
| [lookup_accounts](witness_node/lookupaccounts.md) | &lt;limit&gt; &lt;lower_bound_name&gt; | Acquire the name and ID of registered accounts |  |
| get_account_count |  | Acquire the quantity of accounts which are registered on the chain |  |
| [get_account_balances](witness_node/getaccount-balances.md) | &lt;id&gt; &lt;assets&gt; | Acquire the account asset information by account ID and asset ID |  |
| get_named_account_balances | &lt;name&gt; &lt;assets&gt; | Acquire the account asset information by the account name and asset ID |  |
| get_balance_objects | &lt;&lt;\[address\]&gt;&gt; | Return all the balance objective which has not been received on the address |  |
| get_vested_balances | &lt;objs&gt; | Acquire the accessible asset information by the account balance ID |  |
| get_vesting_balances | &lt;account_id&gt; | Acquire information of the balance which belongs to the account but not accessible temprorarily by the account ID |  |
| list_data_transaction_complain_requesters | &lt;start_date_time&gt; &lt;end_date_time&gt; &lt;limit&gt; | Find the complaint initiator by the starting and ending time meanwhile return the first "limit" |  |
| list_data_transaction_complain_datasources | &lt;start_date_time&gt; &lt;end_date_time&gt; &lt;limit&gt; | Acquire the data source which is complained by the starting and ending time meanwhile return the first "limit" |  |
| get_assets | &lt;asset_ids&gt; | Acquire the asset by asset ID |  |
| [list_assets](witness_node/listassets.md) | &lt;lower_bound_symbol&gt; &lt;limit&gt; | Acquire the asset information by asset symbol name and return the first "limit" |  |
| lookup_asset_symbols | &lt;symbols_or_ids&gt; | Acquire the asset list by asset symbol |  |
| get_witnesses | &lt;witness_ids&gt; | Acquire the witness list by witness ID |  |
| get_witness_by_account | &lt;account&gt; | Acquire the witness information by account ID |  |
| lookup_witness_accounts | &lt;lower_bound_name&gt; &lt;limit&gt; | Acquire the ID and name of the registered witness |  |
| get_witness_count |  | Acquire the qunatity of the registered witness |  |
| get_committee_members | &lt;committee_member_ids&gt; | Acquire the information of the committee member by ID |  |
| get_committee_member_by_account | &lt;account&gt; | Acquire the information of the committee member by account ID |  |
| lookup_committee_member_accounts | &lt;account&gt; &lt;limit&gt; | 获得已注册理事会成员的ID和账户名,并返回前limit个 |  |
| get_workers_by_account | &lt;account&gt; | 通过账户ID获取工作对象信息 |  |
| lookup_vote_ids | &lt;votes&gt; | 通过投票对象ID来获得投票对象 |  |
| get_transaction_hex | &lt;trx&gt; | 获取签名的交易信息的十六进制编码 |  |
| get_required_signatures | &lt;trx&gt; &lt;available_keys&gt; | 获取签名的交易信息的签名公钥 |  |
| get_potential_signatures | &lt;trx&gt; | 获取签名的交易信息的签名公钥 |  |
| get_potential_address_signatures | &lt;trx&gt; | 获取签名的交易信息的地址 |  |
| verify_authority | &lt;trx&gt; | 验证交易是否已满足全部签名要求 |  |
| verify_account_authority | &lt;name_or_id&gt; &lt;signers&gt; | 验证签名人是否有足够的权力控制一个帐户 |  |
| validate_transaction | &lt;trx&gt; | 在当前情况下验证交易而不广播交易 |  |
| get_required_fees | &lt;ops&gt; &lt;id&gt; | 通过操作ID和资产ID获取手续费 |  |
| get_proposed_transactions | &lt;id&gt; | 通过具体账户ID获得相关的被提议的交易 |  |
| get_blinded_balances | &lt;id&gt; | 通过委托ID获取隐藏资产 |  |
| get_data_transaction_product_costs | &lt;start&gt; &lt;end&gt; | 获取指定时间内数据交易的产品费用 |  |
| get_data_transaction_total_count | &lt;start&gt; &lt;end&gt; | 获取指定时间内数据交易的次数 |  |
| get_merchants_total_count |  | 获取当前商户个数 |  |
| get_data_transaction_commission | &lt;start&gt; &lt;end&gt; | 获取指定时间内数据交易的佣金 |  |
| get_data_transaction_pay_fee | &lt;start&gt; &lt;end&gt; | 获取指定时间内数据交易的手续费 |  |
| get_data_transaction_product_costs_by_requester | &lt;requester&gt; &lt;start&gt; &lt;end&gt; | 获取请求账户（即商户）在指定时间内数据交易产生的产品费用 |  |
| get_data_transaction_total_count_by_requester | &lt;requester&gt; &lt;start&gt; &lt;end&gt; | 获取请求账户（即商户）在指定时间内发起数据交易的次数 |  |
| get_data_transaction_pay_fees_by_requester | &lt;requester&gt; &lt;start&gt; &lt;end&gt; | 获取请求账户（即商户）在指定时间内发起数据交易的手续费 |  |
| get_data_transaction_product_costs_by_product_id | &lt;product_id&gt; &lt;start&gt; &lt;end&gt; | 获取在指定时间内购买指定产品的产品费用 |  |
| get_data_transaction_total_count_by_product_id | &lt;product_id&gt; &lt;start&gt; &lt;end&gt; | 获取在指定时间内购买指定产品的次数 |  |
|  |  |  |  |

### history api

| Command | Parameter | Explanation | Note |
| :--- | :--- | :--- | :--- |
| get_account_history | &lt;account_id&gt; &lt;start&gt; &lt;limit&gt; &lt;stop&gt; | 查询帐户的交易历史，其中start/stop为operation_history_id， id为1.11.x |  |
| get_account_history_by_operations | &lt;account_id&gt; &lt;operation_ids&gt; &lt;start&gt; &lt;limit&gt; | 查询帐户的交易历史，根据operations_ids筛选指定类型的交易历史，其中start为序号，从1开始 |  |
